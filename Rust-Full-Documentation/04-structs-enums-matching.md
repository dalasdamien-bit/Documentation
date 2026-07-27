# 🧱 Structs, Enums & Pattern Matching

Combine data and behavior using custom types, Option<T>, and type-safe pattern matching.

---

## 🏛️ 1. Struct Types

```rust
// Standard Struct
struct User {
    username: String,
    email: String,
    active: bool,
}

// Struct Field Init Shorthand & Update Syntax
let user2 = User {
    email: String::from("new@example.com"),
    ..user1 // Copies/moves remaining fields from user1
};

// Tuple Structs & Unit Structs
struct Color(i32, i32, i32);
struct AlwaysEqual;
```

---

## 🔀 2. Enums & `Option<T>`

Rust enums can embed data directly inside variants:

```rust
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}

let home = IpAddr::V4(127, 0, 0, 1);
```

### 🚫 No Nulls: `Option<T>`
Rust replaces `null` with the standard `Option<T>` enum:
```rust
enum Option<T> {
    Some(T),
    None,
}
```

---

## 🎯 3. Control Flow: `match`, `if let`, `let...else`

### Standard Exhaustive `match`
```rust
match option_val {
    Some(i) => println!("Value: {i}"),
    None => println!("Empty"),
}
```

### Concise `if let`
```rust
if let Some(max) = config_max {
    println!("Max is configured to {max}");
}
```

### Happy-Path Guard: `let...else` (v0.16+)
```rust
let Some(user) = fetch_user() else {
    return Err("User not found"); // Must diverge or return
};
println!("Welcome {}", user.name);
```
