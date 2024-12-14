---
tags:
- python
video-url: https://www.youtube.com/watch?v=2hWR06BVSg8&list=WL&index=2
---
## **Python DataClasses

**Overview of Python Data Classes**

Python's `dataclasses` module, introduced in Python 3.7, provides a way to define classes with less boilerplate code. They are particularly useful for creating classes that are primarily used to store data. Below is a detailed explanation of how to use `dataclasses`, including code examples and best practices.

### What Are Data Classes?

Data classes reduce the need for boilerplate code by auto-generating special methods like `__init__`, `__repr__`, `__eq__`, and others. These classes are useful for scenarios where classes are mainly used to hold state.

---

### How to Use Data Classes

#### Basic Setup

```python
from dataclasses import dataclass

@dataclass
class Profile:
    name: str
    age: int
    gender: str
    jobs: list[str]
```
**Explanation:**
1. Use the `@dataclass` decorator to indicate a class is a data class.
2. Define attributes with type hints. Type hints are mandatory for data classes.
3. The `dataclass` module auto-generates an initializer (`__init__`) and other methods based on the fields provided.

#### Example Usage

```python
profile = Profile(name="Ethan", age=26, gender="Male", jobs=["Developer", "Writer"])
print(profile)
```
**Output:**
```
Profile(name='Ethan', age=26, gender='Male', jobs=['Developer', 'Writer'])
```

---

### Features of Data Classes

#### 1. Auto-Generated Methods

- **`__init__`:** Automatically creates an initializer.
- **`__repr__`:** Provides a string representation.
- **`__eq__`:** Allows comparison of objects based on their fields.

#### 2. Default Values and Default Factories

To avoid common issues with mutable defaults, use `default_factory`:

```python
from dataclasses import dataclass, field

default_jobs = field(default_factory=list)

@dataclass
class Profile:
    name: str
    age: int
    gender: str
    jobs: list[str] = default_jobs
```
**Benefit:** Prevents shared mutable default objects.

#### 3. Options in the Decorator

```python
@dataclass(init=True, repr=True, eq=True, order=False, frozen=False)
class Profile:
    name: str
    age: int
    gender: str
    jobs: list[str]
```
**Explanation:**
- `init`: Whether to auto-generate `__init__`.
- `repr`: Whether to auto-generate `__repr__`.
- `eq`: Whether to auto-generate `__eq__`.
- `order`: Enables ordering (`__lt__`, `__gt__`, etc.).
- `frozen`: Makes the class immutable.

#### 4. Field-Specific Options

You can override behavior for specific fields using the `field` function.

```python
from dataclasses import field

default_jobs = field(default_factory=list, repr=False, compare=False)

@dataclass
class Profile:
    name: str
    age: int
    gender: str
    jobs: list[str] = default_jobs
```
**Options:**
- `repr`: Exclude from string representation.
- `compare`: Exclude from equality checks.
- `hash`: Exclude from hashing.
- `kw_only`: Restrict to keyword-only arguments (Python 3.10+).

#### 5. Immutable Data Classes

Set `frozen=True` to make a data class immutable:

```python
@dataclass(frozen=True)
class Profile:
    name: str
    age: int
    gender: str
```

Attempting to modify an instance will raise a `FrozenInstanceError`.

#### 6. Post-Initialization Processing

The `__post_init__` method allows you to perform operations after the instance is created:

```python
@dataclass
class Profile:
    name: str
    age: int
    gender: str

    def __post_init__(self):
        if self.age < 0:
            raise ValueError("Age must be a positive number")
```

---

### Advanced Features

#### Keyword-Only Arguments

Enforce keyword-only arguments:

```python
@dataclass(kw_only=True)
class Profile:
    name: str
    age: int
```
**Usage:**
```python
profile = Profile(name="Ethan", age=26)  # Must use keyword arguments.
```

#### Slots for Memory Efficiency

Use `slots=True` (Python 3.10+) to limit attributes:

```python
@dataclass(slots=True)
class Profile:
    name: str
    age: int
    gender: str
```

#### Hashing

Enable hashing with immutable data classes or by setting `unsafe_hash=True`.

```python
@dataclass(frozen=True, unsafe_hash=True)
class Profile:
    name: str
    age: int
```

---

### Comparison with Alternatives

1. **`attrs`:** More feature-rich but requires installation.
2. **Pydantic:** Designed for data validation with stricter type handling.

---

### Best Practices

1. **Use Type Hints:** Always include type hints for all fields.
2. **Avoid Mutable Defaults:** Use `default_factory` for lists or dictionaries.
3. **Validation:** Use `__post_init__` for complex validations.
4. **Immutable Classes:** Use `frozen=True` if immutability is needed.
5. **Documentation:** Add comments to explain complex `field` configurations.
6. **Python Version Compatibility:** Check compatibility when using features like `slots` or `kw_only`.

---

### Conclusion

Data classes provide a clean and efficient way to define classes in Python, minimizing boilerplate code while maintaining functionality. They are versatile and can be tailored for simple or complex use cases. By understanding the options and best practices, you can effectively utilize data classes in your projects.

[[Python]]