# Concurrency, SIMD Tensors and Blueprints

This guide covers three parts of GlowLang: threads with `spawn`, vectorized tensor math, and
objects with `blueprint`.

---

## 1. Concurrency with `spawn`

`spawn` runs a function on a new operating-system thread. Threads share one global interpreter
lock (GIL): only one thread runs GlowLang code at a time, and the lock is released while a
thread sleeps or waits on the network (`os.sleep`, `os.system`, HTTP and TLS sockets). So
threads let a program **wait on several things at once**; they do not run computations on
several CPU cores in parallel.

```glow
func worker(id):
    os.sleep(100)            # waiting overlaps across threads
    show "Worker finished:", id
end

spawn worker(1)
spawn worker(2)
threads.join_all()          # wait for both (the program also waits at exit)
show "All workers done"
```

For shared work, `lib/async.glow` provides channels, task groups and timers:

```glow
use "lib/async.glow"

let results = Channel("results")
func square(n):
    results.send(n * n)
end
spawn square(3)
spawn square(4)
threads.join_all()
show results.drain()        # [9, 16] (in completion order)
```

---

## 2. SIMD Tensor Math

`tensor` values are flat arrays of numbers. Element-wise `add`, `sub`, `mul`, `dot` and
`matmul` use AVX2 (and FMA for `dot`/`matmul`) when the CPU supports them, and plain scalar code
otherwise; the result is the same either way.

```glow
let v1 = tensor.zeros(1000)
let v2 = tensor.zeros(1000)

let i = 0
while i < 1000:
    v1[i] = 10.5
    v2[i] = 20.5
    i = i + 1
end

let v3 = tensor.add(v1, v2)
show "Result [0]:", v3[0]                  # 31
show "Dot product:", tensor.dot(v1, v2)    # 215250
```

---

## 3. Object-Oriented Blueprints

`blueprint` defines a class; `action` (or `can`, or `func`) defines its methods. `init` runs
when the object is created.

```glow
blueprint HardwareNode:
    action init(node_name):
        self.name = node_name
    end

    action get_status():
        return "ONLINE"
    end
end

let gpu = HardwareNode("GPU-01")
show "Node", gpu.name, "status:", gpu.get_status()
```
