# ⚡ Concurrency & Async/Await

Fearless concurrency through Rust's type system (`Send` & `Sync`), OS threads, and non-blocking futures.

---

## 🧵 1. Multi-Threading & Channels

```rust
use std::thread;
use std::sync::mpsc; // Multiple Producer, Single Consumer

let (tx, rx) = mpsc::channel();

thread::spawn(move || {
    tx.send("Hello from thread").unwrap();
});

let msg = rx.recv().unwrap(); // Blocks until message received
```

### 🔐 Shared State Concurrency
Use **`Arc<Mutex<T>>`** (Atomic Reference Counted Mutex) for thread-safe shared mutable data.

---

## 🚀 2. Async / Await & Futures

Async Rust provides non-blocking, event-driven cooperative multitasking.

```rust
// Futures are LAZY - nothing executes until awaited!
async fn fetch_data() -> String {
    let response = http_get().await;
    response.text().await
}
```

---

## 📌 3. Pin & Unpin Traits

- **`Pin<P>`**: Wraps a pointer to guarantee the underlying data **will not move in memory**. (Required for self-referential async state machines).
- **`Unpin`**: Marker trait indicating a type can safely be moved even when wrapped in `Pin`.

---

## 🌊 4. Streams (Async Iterators)

A stream is an asynchronous sequence of futures over time:

```rust
use trpl::StreamExt;

while let Some(item) = stream.next().await {
    println!("Received: {item}");
}
```
