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

## 3.2 Rust Minimalism

Minimalism reduces complexity, attack surface, and cognitive load.  
VNAGY requires the smallest possible logic that still fulfills the symbolic requirement.

### Bad Example (Over-Engineered)

```rust
fn compute(x: i32) -> i32 {
    let a = x * 2;
    let b = a + 3;
    let c = b * 4;
    c
}
```
Good Example (Minimal)

```rust
fn compute(x: i32) -> i32 {
    x * 2
}
```
Why Bad?

* Unnecessary steps.
  
* Harder to verify.

* Larger attack surface.

Why Good?

* Minimal.

* Deterministic.

* Easy to audit.

3.2.1 Minimalism Verification (Practice)

How developers can verify that code violates minimalism.

Minimalism violations often correlate with nondeterministic behavior, hidden logic, or unnecessary transformations.
Minimalism Test Pattern (Rust)

```rust
fn verify_minimalism<F>(f: F)
where
    F: Fn(i32) -> i32,
{
    let input = 10;
    let output = f(input);
    // A minimal function should have a predictable, linear transformation.
    // Developers manually inspect the function and compare expected vs actual output.
    println!("Input: {}, Output: {}", input, output);
}
```
Why This Helps

* Developers can compare expected vs actual behavior.

* Over-engineered logic becomes visible.

* VNAGY pipelines can reject functions that perform unnecessary transformations.

## 3.3 Explicit Rust State

State MUST be visible, controlled, and local. Global mutable state is strictly forbidden.

### Bad Example (Hidden Global State)

``` rust
static mut COUNTER: u32 = 0;
fn next() -> u32 {
    unsafe {
        COUNTER += 1;
        COUNTER
    }
}
```
### Good Example (Explicit State)

``` rust
struct Counter {
    value: u32,
}

impl Counter {
    fn next(&mut self) -> u32 {
        self.value += 1;
        self.value
    }
}
```
Why Bad?

* Hidden mutation.

* Unsafe block.

* Non-deterministic under concurrency.

Why Good?

* State is explicit.

* No unsafe.

* Predictable behavior.

3.3.1 State Determinism Verification (Practice)

How developers can verify nondeterministic state behavior.

Bad State Test (Global Mutable)

```rust

fn verify_state() {
    let first = next();
    let second = next();
    println!("First: {}, Second: {}", first, second);
}
```
Expected Output

    First: 1, Second: 2

This proves nondeterminism because the output depends on hidden state.

Good State Test (Explicit Struct)

``` rust
fn verify_state() {
    let mut counter = Counter { value: 0 };
    let first = counter.next();
    let second = counter.next();
    println!("First: {}, Second: {}", first, second);
}
```
Expected Output

    First: 1, Second: 2

But here the nondeterminism is explicit, controlled, and predictable.



