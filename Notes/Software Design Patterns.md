---
tags:
- programming
- python
video-url: https://www.youtube.com/watch?v=BJatgOiiht4&list=WL&index=6
---

## **Software Design Patterns

**Overview of Software Design Patterns**

Design patterns provide reusable solutions to common programming problems. Understanding these patterns can enhance code readability, maintainability, and efficiency. Below is a comprehensive guide to several essential design patterns, categorized into **creational**, **structural**, and **behavioral** types.

---

### **Creational Design Patterns**

#### 1. **Singleton Pattern**

- **Definition**: Ensures a class has only one instance and provides a global point of access to it.
- **Use Case**: Logging systems, database connection pools.
- **Pros**:
  - Guarantees a single instance.
  - Provides global access.
- **Cons**:
  - Difficult to test (mocking can be tricky).
  - Requires thread-safe handling in multi-threaded environments.

**Code Example:**
```python
class Singleton:
    _instance = None

    @staticmethod
    def get_instance():
        if Singleton._instance is None:
            Singleton._instance = Singleton()
        return Singleton._instance

# Usage
logger1 = Singleton.get_instance()
logger2 = Singleton.get_instance()
assert logger1 is logger2
```
- **Best Practice**: Use sparingly. Overusing Singletons can lead to tightly coupled code.

---

#### 2. **Builder Pattern**

- **Definition**: Constructs complex objects step-by-step, offering flexibility and readability.
- **Use Case**: Building objects with many optional parameters.
- **Pros**:
  - Improved code readability.
  - Easy to extend.
- **Cons**:
  - More boilerplate code upfront.

**Code Example:**
```python
class RequestBuilder:
    def __init__(self):
        self.url = ""
        self.method = "GET"
        self.headers = {}

    def set_url(self, url):
        self.url = url
        return self

    def set_method(self, method):
        self.method = method
        return self

    def set_headers(self, headers):
        self.headers = headers
        return self

    def build(self):
        return {"url": self.url, "method": self.method, "headers": self.headers}

# Usage
request = RequestBuilder().set_url("https://api.example.com").set_method("POST").set_headers({"Auth": "token"}).build()
```
- **Best Practice**: Use when constructing objects with multiple optional parameters.

---

#### 3. **Factory Pattern**

- **Definition**: Provides an interface for creating objects, delegating instantiation to subclasses.
- **Use Case**: Managing object creation for different types.
- **Pros**:
  - Encapsulates object creation logic.
  - Enhances maintainability.
- **Cons**:
  - Adds a layer of abstraction.

**Code Example:**
```python
class UserFactory:
    @staticmethod
    def create_user(user_type):
        if user_type == "admin":
            return Admin()
        elif user_type == "moderator":
            return Moderator()
        else:
            return RegularUser()

# Usage
user = UserFactory.create_user("admin")
```
- **Best Practice**: Use when object creation logic is complex or varies by type.

---

### **Structural Design Patterns**

#### 1. **Facade Pattern**

- **Definition**: Provides a simplified interface to a complex subsystem.
- **Use Case**: Simplifying interactions with complex subsystems.
- **Pros**:
  - Reduces complexity.
  - Enhances code readability.
- **Cons**:
  - Risk of creating a "god object" that knows too much.

**Code Example:**
```python
class PaymentFacade:
    def place_order(self):
        inventory.check_stock()
        payment.process_payment()
        shipping.schedule_delivery()

# Usage
order = PaymentFacade()
order.place_order()
```
- **Best Practice**: Use when dealing with multiple subsystems to simplify their usage.

---

#### 2. **Adapter Pattern**

- **Definition**: Allows incompatible interfaces to work together by converting one interface into another.
- **Use Case**: Integrating third-party libraries or APIs.
- **Pros**:
  - Encapsulates conversion logic.
  - Enhances compatibility.
- **Cons**:
  - Can be tedious to create adapters for everything.

**Code Example:**
```python
class WeatherAdapter:
    def __init__(self, weather_api):
        self.weather_api = weather_api

    def get_temperature_fahrenheit(self):
        return self.weather_api.get_temperature_celsius() * 9/5 + 32

# Usage
adapter = WeatherAdapter(weather_api_instance)
print(adapter.get_temperature_fahrenheit())
```
- **Best Practice**: Use when adapting third-party components to fit your application’s interface.

---

### **Behavioral Design Patterns**

#### 1. **Strategy Pattern**

- **Definition**: Defines a family of algorithms, encapsulates each, and makes them interchangeable.
- **Use Case**: Switching between different implementations of a process.
- **Pros**:
  - Follows the open/closed principle.
  - Simplifies code by avoiding large conditional statements.
- **Cons**:
  - Increases the number of classes.

**Code Example:**
```python
class TransportStrategy:
    def travel(self):
        pass

class CarStrategy(TransportStrategy):
    def travel(self):
        print("Driving a car.")

class BikeStrategy(TransportStrategy):
    def travel(self):
        print("Riding a bike.")

# Usage
strategy = CarStrategy()
strategy.travel()
```
- **Best Practice**: Use when multiple methods can achieve the same goal.

---

#### 2. **Observer Pattern**

- **Definition**: Allows objects to subscribe to and be notified of events occurring in other objects.
- **Use Case**: Event-driven systems.
- **Pros**:
  - Decouples event producers and consumers.
- **Cons**:
  - Potential for event callback hell.

**Code Example:**
```python
class Observer:
    def update(self, event):
        pass

class Subject:
    def __init__(self):
        self.observers = []

    def subscribe(self, observer):
        self.observers.append(observer)

    def notify(self, event):
        for observer in self.observers:
            observer.update(event)

# Usage
subject = Subject()
observer = Observer()
subject.subscribe(observer)
subject.notify("Event Occurred")
```
- **Best Practice**: Use for event-driven applications, ensuring not to overuse it to avoid complex dependencies.

---

### **Conclusion**

Design patterns offer robust, reusable solutions for common programming challenges. Understanding when and how to use these patterns can significantly enhance your software's quality and maintainability. Practice implementing these patterns in real-world scenarios to master their nuances.

[[Programming]]  [[Python]]