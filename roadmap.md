# GlowLang Roadmap

## Done

* ✅ Register-based bytecode VM with an x86-64 JIT (Windows x64 and System V ABIs), including
  compilation of hot loops.
* ✅ Natural-language syntax: `show`, `when`/`eif`/`otherwise`, `every`, `is in`, `blueprint`,
  `action`, `ask`.
* ✅ Exact integers of any size, closures, f-strings with expressions, list/dict/string methods.
* ✅ SIMD tensors (AVX2/FMA chosen at run time), SQLite, HTTP server and client, JSON, regular
  expressions, BLAKE3 and SHA-256.
* ✅ `gdu` package manager and the GlowLang-packages registry.
* ✅ Language Server Protocol support and editor integrations (VS Code, Neovim, Sublime, Helix,
  JetBrains).
* ✅ Continuous integration on Windows, Linux (with AddressSanitizer) and macOS; 136 test
  programs with checked output.
* ✅ Faster than CPython 3.13 on every program in the benchmark set (1.4×–5.2×).

## Next

* ⏳ **Multi-core execution** — today threads share a global interpreter lock.
* ⏳ **Generational garbage collector** — a real nursery so short-lived objects are cheap.
* ⏳ **Faster calls and broader JIT coverage** — fewer exits from compiled code to the interpreter.
* ⏳ **Fresh pre-built releases** produced by CI for every platform, including macOS on Apple
  silicon, and signed with a trusted certificate.

## Later

* 🚀 More standard-library modules and community packages.
* 🚀 GPU tensor operations beyond the optional CUDA kernels.
* 🚀 Better debugging and profiling tools.
