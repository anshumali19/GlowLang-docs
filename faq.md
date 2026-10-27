# Frequently Asked Questions

### Is GlowLang interpreted or compiled?
Both. Source code is compiled to bytecode, which a register-based virtual machine runs. Functions
that run often, and loops that run long, are compiled at runtime into native x86-64 machine code
by a JIT compiler; on other CPUs everything runs in the interpreter. Anything the compiled code
cannot handle continues in the interpreter with the same result.

### How fast is it?
On the benchmark set in the core repository, GlowLang finishes 1.4× to 5.2× faster than CPython
3.13 (whole-program time, identical output required). It is much slower than compiled languages
such as C, Go or Rust. The numbers and the script that produces them are in
[benchmarks/RESULTS.md](https://github.com/anshumali19/GlowLang-core/blob/main/benchmarks/RESULTS.md).

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
products and matrix multiplication, and the bundled libraries (`ai`, `glowtorch`, `dataframe`)
provide layers, training loops and CSV loading. CUDA kernels are compiled in only when GlowLang is
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
