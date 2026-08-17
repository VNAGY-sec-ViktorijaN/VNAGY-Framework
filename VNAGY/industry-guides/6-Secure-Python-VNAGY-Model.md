# 6. Secure Python (VNAGY Model)

Mandatory security constraints for Python code within VNAGY offline‑first deterministic systems.

---

## 6.1 No Randomness

### Rule  
Python code **MUST NOT** use nondeterministic randomness in core logic.

### Bad Example

```python
import random

def generate_token():
    return random.randint(1, 999999)
```
Why Bad

* nondeterministic output

* impossible to reproduce pipeline behavior

* breaks deterministic testing

*  PRNG internal state introduces implicit behavior
  

### Good Example

```python
def generate_token(seed: int) -> int:
    return seed  # deterministic token

```
---

## 6.2 No Dynamic Imports
Rule

Dynamic imports (__import__, importlib) MUST NOT be used.

### Bad Example

```python
module = __import__("unsafe_module")
module.run()
```
Why Bad

* unpredictable dependency graph

* breaks static analysis

* increases attack surface

* enables runtime module injection

### Good Example

```python
import safe_module
safe_module.run()
```
---

# 6.3 No Reflection
Rule

Reflection (getattr, setattr, inspect) MUST NOT be used in core logic.

### Bad Example

```python
def call(obj, method):
    return getattr(obj, method)()
```

Why Bad

* unpredictable behavior

* bypasses explicit interface contracts

* breaks static verification

* enables unauthorized method invocation

### Good Example

```python
def call_safe(obj):
    return obj.run()
```

---

# 6.4 No Runtime Code Generation
Rule

Runtime code generation (eval, exec) MUST NOT exist.

### Bad Example

```python
def execute(code: str):
    exec(code)
```

Why Bad

* highest‑risk Python construct

* enables arbitrary code execution

* impossible to verify deterministically

*  breaks offline‑first security guarantees

### Good Example

```python
def execute_safe(operation: str):
    if operation == "start":
        return "started"
    raise ValueError("Invalid operation")
```

---

## 6.5 No Global State
Rule

Global mutable state MUST NOT exist.

### Bad Example

```python
counter = 0

def increment():
    global counter
    counter += 1
    return counter
```

Why Bad

* nondeterministic across executions

* breaks isolation

* impossible to test reproducibly

* introduces hidden dependencies

### Good Example

```python
def increment(value: int) -> int:
    return value + 1
```

---

# 6.6 No Heuristics
Rule

Heuristic logic MUST NOT be used in core detection, scoring, or behavior pipelines.

### Bad Example

```python
def classify(event):
    if "suspicious" in event:
        return "alert"
    return "ok"
```

Why Bad

* heuristic pattern matching is nondeterministic

* produces inconsistent results

* cannot be formally verified

* breaks VNAGY deterministic scoring model
  

### Good Example

```python
def classify(event: dict):
    if event["score"] >= 80:
        return "alert"
    return "ok"
```

---

## 6.7 No Operational Logic
Rule

Python code MUST NOT contain operational logic (network calls, filesystem writes, external dependencies) inside core modules.

### Bad Example

```python
import requests

def fetch_data():
    return requests.get("https://example.com").text
```

Why Bad

* breaks offline‑first model

* introduces nondeterministic external dependencies

* impossible to test deterministically

* violates VNAGY isolation rules

### Good Example

```python
def process(data: str) -> str:
    return data.lower()
```

---

## 6.8 Deterministic Pipelines Only
Rule

All pipelines MUST be deterministic, reproducible, and free of implicit behavior.

### Bad Example

```python
def pipeline(data):
    return data + str(random.random())
```

Why Bad

* nondeterministic output

* breaks reproducibility

* invalidates scoring and behavior models

* impossible to verify offline

### Good Example

```python
def pipeline(data: str) -> str:
    return
```

# Licensing

Licensed under VNAGY CC BY‑NC 4.0 Extended License.
Short documents may use VNAGY Minimal License (PSDL‑1.3).
© Viktorija Nađ, 2026 — All Rights Reserved.

License files are available here:
https://github.com/VNAGY-sec-ViktorijaN/VNAGY-Framework/tree/main/VNAGY/LICENSE




