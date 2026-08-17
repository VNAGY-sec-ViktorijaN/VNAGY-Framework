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

---

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

#### 3.2.1 Minimalism Verification (Practice)

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

---

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

#### 3.3.1 State Determinism Verification (Practice)

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

---

## 3.4 Static Rust Structure

Rust modules MUST be statically defined.  
VNAGY forbids dynamic dispatch, dynamic module loading, or runtime‑generated behavior.

### **Bad Example (Dynamic Dispatch)**

```rust
trait Action {
    fn run(&self);
}

fn execute(action: &dyn Action) {
    action.run();
}
```

### **Good Example (Static Call)**

```rust
fn execute() {
    // static, deterministic behavior
}
```

---

#### 3.4.1 Static Structure Verification (Enterprise Practice)

 **Static Structure Test Pattern**

```rust
fn verify_static<F>(f: F)
where
    F: Fn() -> i32,
{
    let first = f();
    let second = f();

    if first != second {
        println!("Dynamic behavior detected.");
    } else {
        println!("Static behavior confirmed.");
    }
}
```

---

## 3.5 Rust Error Handling (Symbolic)

Error handling MUST be:

- explicit  
- deterministic  
- symbolic  
- fail‑fast  
- without fallback heuristics  

### **Bad Example (Implicit Fallback)**

```rust
fn parse(x: &str) -> i32 {
    x.parse().unwrap_or(0)
}
```

### **Good Example (Explicit Error Enum)**

```rust
#[derive(Debug)]
enum ParseError {
    InvalidFormat,
}

fn parse(x: &str) -> Result<i32, ParseError> {
    x.parse::<i32>().map_err(|_| ParseError::InvalidFormat)
}
```


#### 3.5.1 Error Determinism Verification (Practice)

### **Bad Error Test (Silent Fallback)**

```rust
fn verify_error() {
    let first = parse("abc");
    let second = parse("abc");
    println!("First: {}, Second: {}", first, second);
}
```

**Expected Output**

```
First: 0, Second: 0
```

### **Good Error Test (Explicit Enum)**

```rust
fn verify_error() {
    let first = parse("abc");
    let second = parse("abc");
    println!("First: {:?}, Second: {:?}", first, second);
}
```

**Expected Output**

    First: Err(InvalidFormat), Second: Err(InvalidFormat)

Why This Matters

* Developers can see the failure.

* No silent fallback.

* VNAGY pipelines can reject hidden error logic.

# Licensing

Licensed under VNAGY CC BY‑NC 4.0 Extended License.

Short documents may use VNAGY Minimal License (PSDL‑1.3).
© Viktorija Nađ, 2026 — All Rights Reserved.

License files are available here:
https://github.com/VNAGY-sec-ViktorijaN/VNAGY-Framework/tree/main/VNAGY/LICENSE

