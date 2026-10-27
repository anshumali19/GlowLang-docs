# GlowLang Native Modules

Several modules are implemented in C inside the GlowLang runtime, so they need no packages. This
page shows five of them; a runnable pipeline that uses all five is in
[GlowLang-examples/flagship_showcase](https://github.com/anshumali19/GlowLang-examples/tree/main/flagship_showcase).

## 1. BLAKE3 and SHA-256 hashing (`crypto`)
`crypto.blake3` is the standard 256-bit BLAKE3 hash (it matches the official test vectors);
`crypto.sha256` and `crypto.hmac` use OpenSSL.
```glow
let seal = crypto.blake3("Transaction 8821")
show seal               # 64 hex digits
show crypto.sha256("abc")
```

## 2. INT4 weight unpacking (`tensor.dequantize_int4`)
Each element of the input tensor holds one byte that packs two 4-bit weights; the result has
twice as many elements, each in the range -8 to 7.
```glow
let packed = tensor.zeros(1)
tensor.set(packed, 0, 163)                  # 0xA3
show tensor.dequantize_int4(packed)         # [-5, 2]
```

## 3. JSON (`json`)
`json.parse` and `json.stringify` convert between JSON text and GlowLang values.
`json.scan_fast` is a lighter helper that returns only the first key and its value without
parsing the rest of the text.
```glow
let raw = '{"txn": "SOV-8821", "amount": 1000000}'
show json.parse(raw)["amount"]
show json.scan_fast(raw)            # {"key": "txn", "val": "SOV-8821"}
```

## 4. Socket readiness (`net_fast.poll_fast`)
`net_fast.poll_fast(socket, timeout_ms)` returns `true` when a socket has data or a connection
waiting, waiting up to `timeout_ms` (it uses `select`).
```glow
let server = http.listen(8080)
if net_fast.poll_fast(server, 100):
    let client = http.accept(server)
end
```

## 5. PNG image size (`media.png_dims`)
Reads the width and height from the first 24 bytes of a PNG file (stored one byte per element in
a tensor).
```glow
let size = media.png_dims(header_bytes)
show size["width"], size["height"]
```
