# 5. Python Coding Standard (VNAGY Secure Python)

Deterministic, Minimal, Explicit, Static, Symbolic

Python is a dynamic language, but the VNAGY model requires **deterministic, minimal, explicit, static, symbolic** usage.  
This means:

- no randomness  
- no implicit I/O  
- no global mutable state  
- no reflection  
- no dynamic dispatch  
- no runtime code generation  
- no heuristics  
- no fallback logic  

Python is used **symbolically**, not operationally.

---

## 5.1 Python Determinism

Determinism is a VNAGY foundation: **identical input → identical output**.  
Python allows nondeterministic behavior, but VNAGY prohibits it.

### Bad Example (Non‑Deterministic)

```python
import random

def adjust(x: int) -> int:
    return x + random.randint(0, 5)
```

Good Example (Deterministic)
```python
def adjust(x: int) -> int:
    return x + 2
```

Why Bad?

* Randomness breaks determinism — output varies per execution.

* Impossible to reproduce — nondeterministic paths violate offline‑first reproducibility.

* Violates VNAGY predictability — symbolic pipelines require identical results.

Why Good?

* Fully deterministic — identical inputs → identical outputs.

* Minimal and explicit — no hidden logic.

* Offline‑first safe — reproducible across all environments.

5.1.1 Determinism Verification
Determinism Test Pattern (Python)

```python
def verify_determinism(f):
    input_value = 10
    first = f(input_value)
    second = f(input_value)

    if first != second:
        print(f"Nondeterministic: {first} vs {second}")
    else:
        print("Deterministic.")
```
Usage

    python
    verify_determinism(adjust)

---

## 5.2 Python Minimalism

Minimalism reduces complexity, attack surface, and cognitive load.
VNAGY requires the smallest correct transformation.

### Bad Example (Over‑Engineered)

```python
def compute(x: int) -> int:
    a = x * 2
    b = a + 3
    c = b * 4
    return c
```

### Good Example (Minimal)

```python
def compute(x: int) -> int:
    return x * 2
```

Why Bad?

* Unnecessary steps — more logic = more defects.

* Harder to verify — symbolic pipelines require minimal transformations.

* Larger attack surface — complexity increases risk.

Why Good?

* Minimal — smallest correct transformation.

* Deterministic — no hidden behavior.

* Easy to audit — symbolic and predictable.

5.2.1 Minimalism Verification
Minimalism Test Pattern

```python
def verify_minimalism(f):
    input_value = 10
    output = f(input_value)
    print(f"Input: {input_value}, Output: {output}")
```

---

# 5.3 Explicit Python State

State MUST be:

    local

    visible

    controlled

    deterministic

Global mutable state is strictly forbidden.

### Bad Example (Hidden Global State)
python

counter = 0

def next():
    global counter
    counter += 1
    return counter

### Good Example (Explicit State)

```python
class Counter:
    def __init__(self):
        self.value = 0

    def next(self):
        self.value += 1
        return self.value
```

Why Bad?

* Hidden mutation — unpredictable behavior.

* Unsafe concurrency — global variables break determinism.

* Non‑deterministic output — depends on hidden state.

Why Good?

* State is explicit — visible and controlled.

* No global mutation — predictable behavior.

* Deterministic — reproducible across runs.

5.3.1 State Determinism Verification

### Bad State Test

```python
def verify_state():
    first = next()
    second = next()
    print(f"First: {first}, Second: {second}")
```

### Good State Test

```python
def verify_state():
    counter = Counter()
    first = counter.next()
    second = counter.next()
    print(f"First: {first}, Second: {second}")
```

---

## 5.4 Static Python Structure

Python is dynamic, but VNAGY requires static structure:

    no dynamic dispatch

    no reflection

    no runtime module loading

    no runtime code generation

### Bad Example

```python
class Action:
    def run(self):
        pass

def execute(action: Action):
    action.run()
```

### Good Example (Static Call)

```python
def execute():
    return 42  # static, deterministic behavior
```

Why Bad?

* Runtime variability — unpredictable execution paths.

* Harder to verify offline.

* Violates VNAGY static structure rule.

Why Good?

* Fully static.

* Predictable execution path.

*  Easy to audit.

## 5.5 Error Determinism Verification

### Bad Error Test

```python
def verify_error():
    first = parse("abc")
    second = parse("abc")
    print(first, second)
```
### Good Error Test

```python
def verify_error():
    first = parse("abc")
    second = parse("abc")
    assert first == second
```

# Licensing

Licensed under VNAGY CC BY‑NC 4.0 Extended License.

Short documents may use VNAGY Minimal License (PSDL‑1.3). © Viktorija Nađ, 2026 — All Rights Reserved.

License files are available here: https://github.com/VNAGY-sec-ViktorijaN/VNAGY-Framework/tree/main/VNAGY/LICENSE


