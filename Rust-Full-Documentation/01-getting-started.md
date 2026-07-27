# 🦀 Getting Started & Cargo CLI Reference

Rust provides **memory safety without garbage collection**, high-level ergonomics, and zero-cost abstractions.

---

## 🛠️ 1. Installation (`rustup`)

Install the official Rust compiler toolchain using `rustup`:

```bash
# Linux / macOS
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh

# Update Rust to the latest stable version
rustup update

# Check version
rustc --version
```

---

## 📦 2. Cargo Package Manager Cheat-Sheet

Cargo is Rust's build system and package manager.

| Command | Action | Output Location |
| :--- | :--- | :--- |
| `cargo new app_name` | Creates a new project with `Cargo.toml` and `src/main.rs` | `./app_name/` |
| `cargo check` | Fast syntax/type check without producing binaries | N/A (Fastest loop) |
| `cargo build` | Compiles debug build with debug symbols | `target/debug/app_name` |
| `cargo run` | Compiles & executes debug binary | Terminal output |
| `cargo build --release` | Compiles fully optimized production build | `target/release/app_name` |
| `cargo doc --open` | Builds & opens local offline API documentation | Browser window |

---

## 📄 3. Anatomy of `Cargo.toml`

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2024"

[dependencies]
rand = "0.8.5"
```

---

## 🔍 4. Hello World Program Structure

```rust
fn main() {
    // println! calls a Rust macro (not a function). Notice the '!'
    println!("Hello, world!");
}
```
