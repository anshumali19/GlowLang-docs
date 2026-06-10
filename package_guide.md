# GlowLang Package Guide

GlowLang features a built-in package manager called `gdu` (Glow Developer Utility). `gdu` makes it simple to install, verify, and use external packages.

## Installing GlowLang & Packages

`gdu` is not just for packages—it can also manage the GlowLang toolchain itself!
```bash
gdu install glowlang
```

To install a package, use the `gdu` tool from the terminal:

```bash
gdu install http
```

This command will reach out to the official `GlowLang-packages` registry, fetch the package, and install it into your local `~/.glow_pkg` directory.

## Using a Package

Once installed, simply `use` the package by its name in your `.glow` file:

```glow
use "http"

let server = http.Server()
server.listen(8080)
```

## Creating Your Own Package

1. Create a GitHub repository for your code.
2. Ensure your entry point is clearly defined.
3. Write a `package.json` file.
4. Submit a Pull Request to [GlowLang-packages](https://github.com/anshumali19/GlowLang-packages).

If approved by the Core Maintainers, your package will be globally available via `gdu install <your_package>`!
