# GlowLang Flagship Hardware Acceleration Subsystems

GlowLang ships with 5 zero-dependency hardware C/SIMD acceleration subsystems designed to outperform Python, Go, and Rust out-of-the-box.

## 1. `crypto_fast` & `GlowKavach` (Post-Quantum Cryptography & BLAKE3)
Built-in bitwise diffusion engine eliminating OpenSSL dependencies.
```glow
let seal = crypto.blake3("Enterprise Transaction")
```

## 2. `llm` & `GlowVeda` (Quantized INT4 GGUF Neural Engine)
Built-in 4-bit weight dequantization and scaled dot-product attention.
```glow
let weights = tensor.dequantize_int4(int4_buffer)
```

## 3. `simd_json` & `GlowPrism` (Zero-Copy Structural Parser)
AVX2-inspired scanning without temporary heap dictionary bloat.
```glow
let rec = json.scan_fast(raw_payload)
```

## 4. `io_uring` (High-Concurrency Epoll Engine)
Asynchronous event check primitives (`net_fast.poll_fast()`).

## 5. `media` (SIMD Computer Vision & Audio)
Instantaneous raw header decoding (`media.png_dims()`).
