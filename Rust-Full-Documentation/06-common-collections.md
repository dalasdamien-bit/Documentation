# 📚 Common Collections Reference

Heap-allocated data structures for storing dynamic collections of items.

---

## 1. Vector (`Vec<T>`)

```rust
// Initialize
let mut v: Vec<i32> = Vec::new();
let v2 = vec![1, 2, 3]; // Macro shorthand

// Push & Safe Retrieval
v.push(5);
let third: Option<&i32> = v.get(2); // Returns None if out of bounds (No panic)

// Mutable Iteration
for i in &mut v {
    *i += 50; // Dereference operator '*' to mutate
}
```

---

## 2. String (`String` & `&str`)

Strings are UTF-8 encoded wrappers around `Vec<u8>`. Direct integer indexing (`s[0]`) is **forbidden** because UTF-8 characters vary from 1 to 4 bytes in length!

### 🔍 3 Ways to View a String:
1. **Bytes**: `.bytes()` (`[224, 164, 168...]`)
2. **Unicode Scalar Values (`char`)**: `.chars()` (`['न', 'म', 'स'...]`)
3. **Grapheme Clusters**: (Human letters, available via external crates)

```rust
let mut s = String::from("Hello");
s.push_str(", world!");
s.push('!');

// Concatenation with format!
let s3 = format!("{s1}-{s2}");
```

---

## 3. Hash Map (`HashMap<K, V>`)

Stores key-value mappings using SipHash.

```rust
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);

// Insert only if key is absent using entry() API
scores.entry(String::from("Yellow")).or_insert(50);

// Look up value safely
let score = scores.get("Blue").copied().unwrap_or(0);
```
