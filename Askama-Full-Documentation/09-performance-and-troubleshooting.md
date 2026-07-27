# ⚡ Performance Tuning & `FastWritable`

Askama is engineered for high-throughput rendering.

---

## 📊 Rendering Method Benchmarks

| Method | Speed Comparison | Recommended Use Case |
| :--- | :--- | :--- |
| `.render()` | 🚀 100% (Baseline) | Standard web responses (`String`) |
| `.render_into(&mut buf)` | ⚡ 110% Faster | Reusing pre-allocated string buffers |
| `.write_into(&mut writer)` | ⚡ 110% Faster | Writing directly to TCP / HTTP sockets |
| `.to_string()` | 🐢 100% - 200% Slower | **Avoid** (uses dynamic dispatch) |

---

## 🏎️ `FastWritable` Trait Specialization

Custom struct fields rendered via `{{ my_struct }}` normally use `fmt::Display`. Implement `FastWritable` to bypass dynamic vtable calls:

```rust
use askama::{FastWritable, NO_VALUES};
use std::fmt;

struct UserBadge<'a> {
    username: &'a str,
}

impl FastWritable for UserBadge<'_> {
    fn write_into(
        &self,
        dest: &mut dyn fmt::Write,
        _values: &dyn askama::Values,
    ) -> askama::Result<()> {
        dest.write_str("@")?;
        dest.write_str(self.username)?;
        Ok(())
    }
}
```

---

## ⏩ Accelerating Compile Times

If template recompilation is slow during development, optimize the derive proc-macro in `Cargo.toml`:

```toml
[profile.dev.package.askama_derive]
opt-level = 3
```
