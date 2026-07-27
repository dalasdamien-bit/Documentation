# 🚨 Error Handling Reference

Rust categorizes errors into **Unrecoverable** (`panic!`) and **Recoverable** (`Result<T, E>`).

---

## 🛑 1. Unrecoverable Errors (`panic!`)

Used when bugs occur or code enters an invalid state.

```rust
panic!("Crash and burn");
```

- **Stack Unwinding**: Default behavior (cleans up stack memory).
- **Immediate Abort**: Set `panic = 'abort'` in `Cargo.toml` under `[profile.release]` for tiny binary sizes.
- **Backtrace Debugging**: Run terminal with `RUST_BACKTRACE=1 cargo run`.

---

## 🛡️ 2. Recoverable Errors (`Result<T, E>`)

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

### Shortcuts for Panic on Error
- `.unwrap()`: Returns `T` if `Ok`, panics if `Err`.
- `.expect("Custom error message")`: Returns `T` if `Ok`, panics with custom message if `Err` (Preferred for production code).

---

## ❓ 3. Error Propagation with `?`

The `?` operator unwraps `Ok(val)` or performs an **early return** of `Err(e)` from the current function:

```rust
fn read_username() -> Result<String, io::Error> {
    let mut s = String::new();
    File::open("hello.txt")?.read_to_string(&mut s)?;
    Ok(s)
}
```

*Note: `main()` can also return `Result<(), Box<dyn std::error::Error>>`.*
