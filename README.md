# GlowLang Documentation

Guides for [GlowLang](https://github.com/anshumali19/GlowLang-core), a programming language with
natural-language syntax, a bytecode VM with an x86-64 JIT, and built-in HTTP, SQLite, JSON and
SIMD tensors.

## Contents

* **[Syntax Guide](syntax.md)** — variables, `when`, `every`, blueprints, membership tests
* **[Tutorial: Building a Counter](tutorials.md)** — your first program
* **[Concurrency, SIMD and Blueprints](concurrency_and_simd.md)**
* **[Native Modules](tutorials/flagship_hardware_acceleration.md)** — BLAKE3, JSON, INT4 weights, sockets, PNG headers
* **[Package Manager Guide](package_guide.md)** — installing and publishing packages with `gdu`
* **[Examples](examples.md)**
* **[Roadmap](roadmap.md)**
* **[FAQ](faq.md)**

The complete language reference lives in the core repository:
[docs/language_reference.md](https://github.com/anshumali19/GlowLang-core/blob/main/docs/language_reference.md).

---

## Installing GlowLang

### Pre-built binaries

Download an archive for Windows, Linux or macOS (x64) from the
**[Releases page](https://github.com/anshumali19/GlowLang-packages/releases)**, or let `gdu`
download the latest release and add it to your PATH:

```bash
gdu install glowlang
```

Releases can lag behind the source; build from source for the newest fixes.

### From source

```bash
git clone https://github.com/anshumali19/GlowLang-core.git
cd GlowLang-core
make                # Linux/macOS (gcc, flex, bison, libsqlite3-dev, libssl-dev, libx11-dev)
.\build.bat         # Windows (Visual Studio Build Tools, win_flex/win_bison, vcpkg)
```

Run a program with:

```bash
glowlang run app.glow
```

### Building only `gdu`

```bash
git clone https://github.com/anshumali19/GlowLang-packages.git
cd GlowLang-packages/gdu
gcc gdu.c -o gdu -O2 -lsqlite3 -lcrypto      # or: make
```
