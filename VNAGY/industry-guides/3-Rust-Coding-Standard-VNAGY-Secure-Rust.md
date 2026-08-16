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

### Good Example (Deterministic)
```rust
fn adjust(x: i32) -> i32 {
    x + 2
}
```
Why Bad?

* Randomness breaks determinism.

* Output cannot be reproduced.

* Violates VNAGY offline-first predictability.

Why Good?

* Fully deterministic.

* Minimal and explicit.

* Safe for offline-first pipelines.

#### 3.1.1 Determinism Verification

How developers can verify nondeterministic Rust code.

Determinism Test Pattern (Rust)

```rust
fn verify_determinism<F>(f: F)
where
    F: Fn(i32) -> i32,
{
    let input = 10;
    let first = f(input);
    let second = f(input);

    if first != second {
        println!("Nondeterministic: {} vs {}", first, second);
    } else {
        println!("Deterministic.");
    }
}
```
Usage
```rust
fn main() {
    verify_determinism(adjust);
}
```
Expected Output for Bad Code

    Nondeterministic: 12 vs 14.

Expected Output for Good Code

    Deterministic.

Why This Matters

* Teams can automatically detect nondeterminism.

* Offline-first systems require reproducibility.

* Nondeterministic modules must be rejected.



