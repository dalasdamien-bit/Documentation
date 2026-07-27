# ⚡ Closures & Iterators

Functional programming features providing high-level abstraction with **zero-cost runtime performance**.

---

## 🪢 1. Closures

Anonymous functions that can capture variables from their enclosing environment.

```rust
let add_one = |x: u32| -> u32 { x + 1 };
```

### 🎯 Closure Environment Traits
- **`FnOnce`**: Called at least once; moves captured values out of its body.
- **`FnMut`**: Called multiple times; mutates captured environment variables.
- **`Fn`**: Called multiple times; borrows environment immutably or captures nothing.

### 🚚 The `move` Keyword
Forces closure to take ownership of environment variables:
```rust
thread::spawn(move || println!("Moved vector: {v:?}"));
```

---

## 🔄 2. Iterators (`Iterator` Trait)

Iterators are **lazy**: they do nothing until a consuming adapter is called.

```rust
pub trait Iterator {
    type Item;
    fn next(&mut self) -> Option<Self::Item>;
}
```

### ⚙️ Adapter Methods
- **Consuming Adapters**: Use up the iterator (`.sum()`, `.collect()`, `.count()`).
- **Iterator Adapters**: Produce new iterators (`.map()`, `.filter()`, `.take()`, `.zip()`).

```rust
let v1 = vec![1, 2, 3];

// Chained iterator transformation
let v2: Vec<_> = v1.iter()
    .map(|x| x * 2)
    .filter(|x| *x > 2)
    .collect();
```
