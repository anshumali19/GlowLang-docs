# Frequently Asked Questions

### Is GlowLang interpreted or compiled?
Both. Source code is compiled to bytecode, which a register-based virtual machine runs. Functions
that run often, and loops that run long, are compiled at runtime into native x86-64 or ARM64
machine code by a JIT compiler; on other CPUs everything runs in the interpreter. Anything the
compiled code cannot handle continues in the interpreter with the same result. Memory is managed
by a generational garbage collector.

### How fast is it?
On the benchmark set in the core repository, GlowLang 1.8.0 finishes 1.4× to 8.1× faster than
CPython 3.14 (whole-program time including startup, identical output required). It is much slower
than compiled languages such as C, Go or Rust. The table is in the
[core README](https://github.com/anshumali19/GlowLang-core#-performance), and
`benchmarks/run-benchmarks.sh` (Linux, macOS) and `run-benchmarks.ps1` (Windows) produce it.

### How do I install GlowLang?
On Windows, from the [Microsoft Store](https://apps.microsoft.com/detail/9P2D8F466LBX) or with
`winget install --id 9P2D8F466LBX --source msstore`. On Linux and macOS, download and unpack the
release with one `curl` command: see [Installing GlowLang](README.md#installing-glowlang).

### How do I run a program?
`glowlang run app.glow`, or just `glowlang app.glow`. With no file, `glowlang` opens a REPL, and
`glowlang check app.glow` reports syntax errors without running anything.

### Is GlowLang like Python?
Close. Blocks end with `end` instead of depending on indentation, and keywords such as `show`,
`when`, `every` and `blueprint` read like English, while `if`, `else`, `for each`, `class` and
`print` work too. `//`, `%`, slices, f-strings, comprehensions and named arguments follow
Python's rules, and `...rest` does what `*args` does.

### How do I write a comment?
With `#` to the end of the line, or `/* ... */` across lines. `//` is floor division
(`7 // 2` is `3`), as in Python; it stopped being a comment in 1.8.0.

### Why does GlowLang not use semicolons?
Statements end at the end of the line. Inside open brackets `( [ {` a statement can continue onto
the next lines.

### How do I print something?
Use `show`:
```glow
show "Hello World"
show "x is", x
```
`print` is accepted as another name for `show`.

### Can I do machine learning in GlowLang?
Yes, at a small scale. The `tensor` module has SIMD-accelerated element-wise operations, dot
products and matrix multiplication. Five libraries written in GlowLang cover the usual Python
stack: `glownum` (like NumPy), `glowframe` (like pandas), `glowlearn` (like scikit-learn),
`glowgrad` (autograd and neural networks, like PyTorch) and `glowtext` (text for machine
learning); see [ai_libraries.md](https://github.com/anshumali19/GlowLang-core/blob/main/docs/ai_libraries.md).
The older bundled libraries (`ai`, `glowtorch`, `dataframe`) provide layers, training loops and
CSV loading. CUDA kernels are compiled in only when GlowLang is
built on a machine with NVIDIA's `nvcc`.

### Can threads use several CPU cores?
Not yet. Threads share a global interpreter lock, so they overlap waiting (network, sleep), not
computation. See [Concurrency](concurrency_and_simd.md).

### How do I contribute?
All repositories are public and accept pull requests:
* the language, VM, JIT and standard library: [GlowLang-core](https://github.com/anshumali19/GlowLang-core)
  (see its CONTRIBUTING.md);
* packages: [GlowLang-packages](https://github.com/anshumali19/GlowLang-packages);
* examples and documentation: GlowLang-examples and GlowLang-docs.

### Can I use GlowLang commercially?
Yes. GlowLang is licensed under the Apache License 2.0 with the Commons Clause: you may use it for
any purpose and sell the programs you write with it, but GlowLang itself may not be sold or
patented. See the [LICENSE](https://github.com/anshumali19/GlowLang-core/blob/main/LICENSE).
