# GlowLang Documentation

Guides for [GlowLang](https://github.com/anshumali19/GlowLang-core), a fast, free programming
language with Python-like, natural-language syntax: a bytecode VM with x86-64 and ARM64 JITs, a
generational garbage collector, and built-in HTTP, WebSockets, PostgreSQL, SQLite, JSON and SIMD
tensors. On its benchmark set it runs 1.4× to 7.1× faster than CPython.

The current release is **1.12.0** ([what's new](https://github.com/anshumali19/GlowLang-core/blob/main/docs/release_notes_1.12.0.md): `glowlang new` for a web API or a command-line tool, `glowlang watch`, `glowlang test`, `glowlang fmt`, one-file programs for any system with `package --target`, error messages that say how to fix the mistake, line editing in the REPL, and concurrent web servers up to 22× faster).

## Contents

* **[Syntax Guide](syntax.md)** — variables, `when`, `every`, blueprints, named arguments, `match`, sets, `??`, `finally`, generators, `with`
* **[Tutorial: Building a Counter](tutorials.md)** — your first program
* **[Concurrency, SIMD and Blueprints](concurrency_and_simd.md)**
* **[Native Modules](tutorials/flagship_hardware_acceleration.md)** — BLAKE3, JSON, INT4 weights, sockets, PNG headers
* **[Package Manager Guide](package_guide.md)** — installing and publishing packages with `gdu`
* **[Examples](examples.md)**
* **[Roadmap](roadmap.md)**
* **[FAQ](faq.md)**

In the core repository:

* **[GlowLang in 10 minutes](https://github.com/anshumali19/GlowLang-core/blob/main/docs/glowlang_in_10_minutes.md)**: the whole language by example
* **[Language reference](https://github.com/anshumali19/GlowLang-core/blob/main/docs/language_reference.md)**: everything else
* **[Getting started](https://github.com/anshumali19/GlowLang-core/blob/main/docs/getting_started.md)**, the [web guide](https://github.com/anshumali19/GlowLang-core/blob/main/docs/web_guide.md), [PostgreSQL](https://github.com/anshumali19/GlowLang-core/blob/main/docs/postgres.md), [WebSockets](https://github.com/anshumali19/GlowLang-core/blob/main/docs/websocket.md), [JWT and OAuth](https://github.com/anshumali19/GlowLang-core/blob/main/docs/jwt_oauth.md) and [AI libraries](https://github.com/anshumali19/GlowLang-core/blob/main/docs/ai_libraries.md)

---

## Installing GlowLang

### Windows

Install from the **[Microsoft Store](https://apps.microsoft.com/detail/9P2D8F466LBX)**, or from a
terminal:

```powershell
winget install --id 9P2D8F466LBX --source msstore
```

The Store version is signed by Microsoft and updates itself; `glowlang` and `gdu` work in every
terminal afterwards.

### Linux (x64)

```bash
mkdir -p ~/glowlang
curl -fsSL https://github.com/anshumali19/GlowLang-packages/releases/latest/download/glowlang-linux-x64.tar.gz | tar -xz -C ~/glowlang
echo 'export PATH="$HOME/glowlang:$PATH"' >> ~/.bashrc && export PATH="$HOME/glowlang:$PATH"
glowlang --version
```

Needs glibc 2.35 or newer (Ubuntu 22.04+, Debian 12+, Fedora 36+), libX11 and SQLite.

### macOS (Apple silicon and Intel)

```bash
arch=$([ "$(uname -m)" = arm64 ] && echo arm64 || echo x64)
mkdir -p ~/glowlang
curl -fsSL https://github.com/anshumali19/GlowLang-packages/releases/latest/download/glowlang-macos-$arch.tar.gz | tar -xz -C ~/glowlang
echo 'export PATH="$HOME/glowlang:$PATH"' >> ~/.zshrc && export PATH="$HOME/glowlang:$PATH"
glowlang --version
```

All downloads, with SHA-256 checksums, are on the
**[Releases page](https://github.com/anshumali19/GlowLang-packages/releases/latest)**. Keep the
`lib/` folder next to `glowlang`.

To update later on Linux or macOS, run `gdu install glowlang`: it installs the latest release in
`~/.glowlang/bin` and adds that folder to your PATH in `~/.bashrc` and `~/.zshrc`.

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
