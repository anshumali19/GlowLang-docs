# Frequently Asked Questions

### Is GlowLang interpreted or compiled?
GlowLang is both! It compiles your code into highly optimized bytecode, which is then executed by our custom Virtual Machine. For performance-critical loops, GlowLang features an experimental JIT (Just-In-Time) compiler that converts bytecode directly into native machine instructions at runtime!

### Why does GlowLang not use semicolons?
We believe code should be as clean and readable as possible. Semicolons are visual clutter. In GlowLang, statements naturally end at the end of the line.

### How do I print something?
Use the `show` keyword! It is cleaner than traditional print statements.
`show "Hello World"`

However, if you are accustomed to Python or C, `print("Hello World")` is perfectly valid and supported.

### Can I do Machine Learning in GlowLang?
Absolutely. GlowLang was built with ML in mind. It features a native SIMD-accelerated Tensor type, meaning you don't need clunky C++ wrappers just to do fast matrix multiplication. We are also actively developing CUDA GPU acceleration.

### How do I contribute?
If you want to write standard packages, submit them to `GlowLang-packages`. If you want to contribute to the core C engine, you will need to apply to become a Trusted Maintainer, as the core repository (`GlowLang-core`) is strictly private to ensure stability and vision alignment.
