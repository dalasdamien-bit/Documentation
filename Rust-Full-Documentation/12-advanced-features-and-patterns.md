# 🔬 Advanced Features & Macros

Low-level systems access, unsafe superpowers, type system extensions, and metaprogramming.

---

## ⚡ 1. Unsafe Rust (5 Superpowers)

1. **Dereference raw pointers** (`*const T`, `*mut T`).
2. **Call unsafe functions or FFI** (`extern "C"`).
3. **Access or modify mutable static variables**.
4. **Implement unsafe traits** (`unsafe impl`).
5. **Access fields of a `union`**.

```rust
let mut num = 5;
let r1 = &raw const num;

unsafe {
    println!("r1: {}", *r1);
}
```

---

## 🧬 2. Advanced Traits & Types

- **Associated Types**: `type Item;` inside trait definitions.
- **Supertraits**: `trait OutlinePrint: fmt::Display` requires `Display` implementation.
- **Newtype Pattern**: `struct Wrapper(Vec<String>);` bypasses the Orphan Rule.
- **Type Aliases**: `type Thunk = Box<dyn Fn() + Send>;`
- **The Never Type (`!`)**: Used for functions that never return (diverging functions).

---

## 🪄 3. Declarative & Procedural Macros

### Declarative Macros (`macro_rules!`)
```rust
macro_rules! vec {
    ( $( $x:expr ),* ) => {
        {
            let mut temp = Vec::new();
            $( temp.push($x); )*
            temp
        }
    };
}
```

### Procedural Macros
Code that operates on token streams at compile time:
1. **Custom `#[derive]`**: Generates trait code for annotated structs.
2. **Attribute-like**: `#[route(GET, "/")]`
3. **Function-like**: `sql!(SELECT * FROM users)`
