# 🔐 Ownership, Borrowing & Slices

Ownership is Rust's most unique feature, guaranteeing **compile-time memory safety** without a garbage collector.

---

## 📜 The 3 Fundamental Rules of Ownership

1. **Each value in Rust has an owner.**
2. **There can only be ONE owner at a time.**
3. **When the owner goes out of scope, the value is automatically dropped (`drop`).**

---

## 🧠 Stack vs. Heap Operations

| Behavior | Stack Data (Fixed Size) | Heap Data (Dynamic Size) |
| :--- | :--- | :--- |
| Examples | `i32`, `f64`, `bool`, `char`, tuples of Copy | `String`, `Vec<T>`, `Box<T>` |
| Assignment (`let b = a`) | **Copy** (Both variables remain valid) | **Move** (Original variable `a` becomes invalidated) |
| Explicit Deep Duplication | Automatic | Requires `.clone()` |

```rust
let s1 = String::from("hello");
let s2 = s1; // s1 is MOVED into s2. s1 is now invalid!

// println!("{s1}"); // ❌ Compile Error: borrow of moved value 's1'
```

---

## 🤝 References & Borrowing Rules

Borrowing allows referencing data without taking ownership using `&`:

### ⚖️ The Borrowing Rule
At any given time, you can have:
- **EITHER** exactly **one mutable reference** (`&mut T`)
- **OR** any number of **immutable references** (`&T`)
- **References must ALWAYS be valid** (No dangling pointers).

```rust
fn calculate_length(s: &String) -> usize {
    s.len()
} // s goes out of scope, but the underlying String is NOT dropped because it was borrowed!
```

---

## 🍕 Slices (`&str` and `&[T]`)

A slice is a reference to a contiguous sequence of elements in a collection without ownership:

```rust
let s = String::from("hello world");

let hello: &str = &s[0..5];
let world: &str = &s[6..11];
let full:  &str = &s[..];
```
