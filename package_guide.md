# GlowLang Package Guide

GlowLang's package manager is `gdu`, the Glow Dependency Utility. It installs packages from the
[GlowLang-packages](https://github.com/anshumali19/GlowLang-packages) registry and can install the
GlowLang toolchain itself.

## Installing GlowLang

```bash
gdu install glowlang
```

This downloads the latest published release into `~/.glowlang/bin` and adds it to your PATH.

## Installing a package

Run `gdu` inside your project folder:

```bash
gdu install json
```

`gdu` downloads `json.glow` into the project's `.glow_pkg/` folder and records `json@1.0.0` in
`Glow.deps`. Running `gdu install` with no name installs everything listed in `Glow.deps`;
`gdu resolve` writes `Glow.lock` with SHA-256 checksums, and `gdu verify` checks them.

## Using a package

Load it by name with `use`:

```glow
use "json"

let data = json.parse('{"user": {"name": "Ada"}}')
show jpath(data).get("user.name")
```

`use "name"` looks for `name.glow` next to your program first, then for an installed package in
`.glow_pkg/`, then in the `lib/` folder that comes with GlowLang.

The `http` package is an HTTP **client**:

```glow
use "http"

let client = HttpClient()
let response = client.get("http://localhost:8080/hello")
show response.status, response.body
```

(To serve HTTP, use the built-in `http.listen` / `http.accept` / `http.send`.)

## Publishing a package

1. Fork [GlowLang-packages](https://github.com/anshumali19/GlowLang-packages).
2. Add `packages/<name>/<name>.glow`, a `package.json` and a `README.md`.
3. Check it with `gdu/package_lint.glow` and test it with the current GlowLang build.
4. Open a pull request (commits signed off with `git commit -s`).

Once a maintainer merges it, anyone can install it with `gdu install <name>`. The full checklist
is in the registry's [CONTRIBUTING.md](https://github.com/anshumali19/GlowLang-packages/blob/main/CONTRIBUTING.md).
