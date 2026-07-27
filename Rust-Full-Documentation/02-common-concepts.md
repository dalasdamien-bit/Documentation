# ⚙️ Common Programming Concepts

Core language building blocks: variables, mutability, primitive types, functions, and control flow.

---

## 📌 Variables, Mutability & Shadowing

| Keyword | Behavior | Type Annotation | Lifetime / Scope |
| :--- | :--- | :--- | :--- |
| `let x = 5;` | **Immutable** by default | Optional (Inferred) | Scope block |
| `let mut y = 5;` | **Mutable** | Optional (Inferred) | Scope block |
| `const MAX: u32 = 100;` | **Always Constant** | **Mandatory** | Entire program run |

### 👤 Variable Shadowing
Shadowing allows re-using a variable name using `let`, even changing its data type:
```rust
let spaces = "   ";          // Type: &str
let spaces = spaces.len();   // Type: usize (Shadows previous variable)
```

---

## 📊 Data Types Summary

### 1. Scalar Types (Single Value)
- **Integers**: Signed (`i8`, `i16`, `i32`, `i64`, `i128`, `isize`), Unsigned (`u8`, `u16`, `u32`, `u64`, `u128`, `usize`)
- **Floats**: `f32`, `f64` (Default)
- **Booleans**: `bool` (`true` / `false`)
- **Characters**: `char` (4 bytes, Unicode scalar value, written with single quotes e.g. `'a'`, `'🦀'`)

### 2. Compound Types
- **Tuple**: Fixed length, heterogeneous types `let t: (i32, f64) = (500, 6.4);`
- **Array**: Fixed length, homogeneous types, allocated on stack `let a: [i32; 5] = [1, 2, 3, 4, 5];`

---

## 🔁 Control Flow Cheat-Sheet

```rust
// 1. If Expression (Arms must return the SAME type)
let number = if condition { 5 } else { 6 };

// 2. Loop with return value
let result = loop {
    counter += 1;
    if counter == 10 {
        break counter * 2; // Returns 20
    }
};

// 3. For Loop over Range / Array
for number in (1..4).rev() {
    println!("{number}!");
}
```
