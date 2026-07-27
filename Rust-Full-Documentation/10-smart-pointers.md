# 🧠 Smart Pointers Reference

Smart pointers are data structures that act like pointers with extra metadata and capabilities.

---

## 📊 Standard Smart Pointers Comparison

| Smart Pointer | Ownership | Borrow Checks | Thread Safety | Primary Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **`Box<T>`** | Single | Compile-time | Safe | Heap allocation, recursive types |
| **`Rc<T>`** | Multiple | Compile-time | Single-threaded | Sharing read-only heap data |
| **`RefCell<T>`** | Single | **Runtime** | Single-threaded | Interior mutability (modify immutable data) |
| **`Arc<T>`** | Multiple | Compile-time | **Thread-safe** | Atomic reference counting across threads |
| **`Mutex<T>`** | Single | **Runtime** | **Thread-safe** | Mutex lock for shared mutable thread state |

---

## 🛠️ Key Traits Behind Smart Pointers

### 1. `Deref` Trait
Allows smart pointers to be treated like regular references (`*` operator). Enables **Deref Coercion** (converting `&String` to `&str` automatically).

### 2. `Drop` Trait
Customizes cleanup code executed when a value goes out of scope:
```rust
impl Drop for CustomPointer {
    fn drop(&mut self) {
        println!("Freeing resources!");
    }
}
```

---

## 🔄 Prevents Cycles: `Weak<T>`
Use `Rc::downgrade(&rc_ptr)` to produce a `Weak<T>` pointer with non-owning references to avoid memory leaks.
