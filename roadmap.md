# GlowLang Roadmap

The current release is **1.9.0** ([release notes](https://github.com/anshumali19/GlowLang-core/blob/main/docs/release_notes_1.9.0.md)).

## Done

* ✅ Register-based bytecode VM with JIT compilers for x86-64 (Windows x64 and System V ABIs) and
  ARM64 (Apple silicon, ARM Linux), including compilation of hot loops.
* ✅ Generational garbage collector: most collections look only at new objects.
* ✅ Natural-language syntax: `show`, `when`/`eif`/`otherwise`, `every`, `is in`, `blueprint`,
  `action`, `ask`.
* ✅ `match` / `case`, `enum`, sets, `try` / `catch` / `finally`, unpacking, named arguments,
  `...rest` / `...spread`, `??` and `?.`, slice steps, bitwise operators, Python-style `//`.
* ✅ Exact integers of any size, closures, f-strings with expressions, list/dict/set/string methods.
* ✅ SIMD tensors (AVX2/FMA chosen at run time), SQLite, PostgreSQL, HTTP server and client,
  WebSockets, JSON, regular expressions, BLAKE3 and SHA-256, JWT and OAuth / OpenID Connect.
* ✅ AI libraries written in GlowLang: `glownum`, `glowframe`, `glowlearn`, `glowgrad`, `glowtext`.
* ✅ `gdu` package manager and the GlowLang-packages registry.
* ✅ Language Server Protocol support and editor integrations (VS Code, Neovim, Sublime, Helix,
  JetBrains).
* ✅ Continuous integration on Windows, Linux (with AddressSanitizer, interpreter-only and GC
  stress runs) and macOS; 231 test programs with checked output.
* ✅ Releases built and tested by CI for Windows x64, Linux x64 and macOS (Apple silicon and
  Intel), and a Microsoft Store version signed by Microsoft.
* ✅ Generators (`yield`, `yield from`, `next`) and `with` blocks for resources (1.9.0).
* ✅ Faster than CPython 3.14 on every program in the benchmark set (1.4×–7.9×).

## Next

* ⏳ **Decorators** (`@cache`, `@route("/")`) and multi-line input in the REPL.
* ⏳ **Faster calls and broader JIT coverage**: named-argument calls resolved when the program
  is compiled, fewer exits from compiled code to the interpreter.
* ⏳ **Multi-core execution**: today threads share a global interpreter lock.
* ⏳ **Signed downloads outside the Store**, so the Windows zip runs without SmartScreen warnings.

## Later

* 🚀 Testing the service clients against the live services (payment, messaging and cloud APIs);
  today they are tested against mock servers that check every request.
* 🚀 More standard-library modules and community packages.
* 🚀 GPU tensor operations beyond the optional CUDA kernels.
* 🚀 Better debugging and profiling tools.
