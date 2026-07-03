# GlowLang Documentation

Welcome to the official documentation for GlowLang!

## Contents
*   **[Syntax Guide](syntax.md)**
*   **[Tutorials](tutorials.md)**
*   **[Package Manager Guide](package_guide.md)**
*   **[Examples](examples.md)**
*   **[Roadmap](roadmap.md)**
*   **[FAQ](faq.md)**

---

## ⚡ Fast Installation via `gdu` (Glow Dependency Utility)
The fastest way to install the entire GlowLang toolchain is using `gdu`.

### 1. Download `gdu`
Download the pre-compiled `gdu` binary for your platform (Linux, macOS, Windows) from the **[GitHub Releases Page](https://github.com/anshumali19/GlowLang-packages/releases)**.

### 2. Run the Installer
Run the following command in your terminal to download, compile, and add the `glowlang` toolchain to your system PATH automatically:

```bash
# On Linux/macOS
gdu install glowlang

# On Windows
gdu.exe install glowlang
```

### 3. Bootstrap from Source (Alternative)
If you do not have a pre-compiled `gdu` binary, you can compile and run `gdu` manually to bootstrap the installation:

```bash
# Clone the packages repository
git clone https://github.com/anshumali19/GlowLang-packages.git
cd GlowLang-packages/gdu

# Compile gdu
gcc gdu.c -o gdu -O2 -lsqlite3

# Install the toolchain
./gdu install glowlang
```
