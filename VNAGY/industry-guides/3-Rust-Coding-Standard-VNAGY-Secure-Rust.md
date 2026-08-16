# 3. Rust Coding Standard (VNAGY Secure Rust)

Deterministic, Minimal, Explicit, Static, Symbolic

---

## 3.1 Rust Determinism

Determinism is a core VNAGY requirement: identical inputs MUST produce identical outputs.  
Rust already encourages deterministic behavior, but VNAGY forbids randomness, implicit IO, hidden state, and dynamic behavior.

### Bad Example (Non-Deterministic)

```rust
use rand::Rng;
fn adjust(x: i32) -> i32 {
    let mut rng = rand::thread_rng();
    x + rng.gen_range(0..5)
}
```

###Good Example (Deterministic)
```rust

fn adjust(x: i32) -> i32 {
    x + 2
}
```
Why Bad?

    Randomness breaks determinism.

    Output cannot be reproduced.

    Violates VNAGY offline-first predictability.

Why Good?

    Fully deterministic.

    Minimal and explicit.

    Safe for offline-first pipelines.

