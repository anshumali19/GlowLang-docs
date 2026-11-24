# GlowLang Roadmap

The current release is **1.13.0** ([release notes](https://github.com/anshumali19/GlowLang-core/blob/main/docs/release_notes_1.13.0.md)).

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
  stress runs) and macOS; 284 test programs with checked output.
* ✅ Releases built and tested by CI for Windows x64, Linux x64 and macOS (Apple silicon and
  Intel), and a Microsoft Store version signed by Microsoft.
* ✅ Generators (`yield`, `yield from`, `next`) and `with` blocks for resources (1.9.0).
* ✅ Decorators on functions and methods (`@cache`), `**opts` / `**dict`, multi-line input in
  the REPL, and named-argument calls matched when the program is compiled (1.10.0).
* ✅ `parallel.map` over worker processes for every core, `close()` for generators, decorators
  on trait methods, named arguments matched when compiling for methods and constructors, and
  functions using `show` or `throw` compiled (1.11.0).
* ✅ Tools: `glowlang new` (a web API or, with `--cli`, a command-line tool), `glowlang watch`
  (restart on save), `glowlang test`, `glowlang fmt`, and `glowlang package --target` to build a
  one-file program for another system; error messages with "did you mean" and the block that is
  missing its `end`; line editing and history in the REPL; spawned threads reused and a GIL
  switch interval, which made concurrent web servers up to 22× faster (1.12.0).
* ✅ Standard modules written in GlowLang: `csv`, `toml`, `yaml`, `dotenv`, `template`, `markdown`,
  `schema`, `url`, `log`, `lru`, `collections`, `semver` and `diff`, each timed against Python;
  GlowWeb keep-alive, cookies and `PATCH` routes; regular expressions compiled once (1.13.0).
* ✅ Faster than CPython 3.14 on every program in the benchmark set (1.4×–6.7×).

## Next

* ⏳ **Threads on several cores**: threads still share a global interpreter lock;
  `parallel.map` uses separate processes instead.
* ⏳ **Signed downloads outside the Store**, so the Windows zip runs without SmartScreen warnings.

## Later

* 🚀 Testing the service clients against the live services (payment, messaging and cloud APIs);
  today they are tested against mock servers that check every request.
* 🚀 More standard-library modules and community packages.
* 🚀 GPU tensor operations beyond the optional CUDA kernels.
* 🚀 Better debugging and profiling tools.
