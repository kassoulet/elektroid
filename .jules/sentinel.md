## 2026-03-24 - [Fix Buffer Overflow in Backend Status]
**Vulnerability:** Potential heap-based buffer overflows in `elektroid_update_backend_status` due to incorrect `n` parameter calculation in `strncat`.
**Learning:** The original code used `sizeof(status)` where `status` was a pointer (`gchar *`), resulting in a constant value (pointer size) instead of the remaining buffer space. This made the code vulnerable if backend name, version, or description were long.
**Prevention:** Use `GString` from GLib for dynamic string building and concatenation. It automatically handles memory management and prevents buffer overflows by resizing the buffer as needed.
