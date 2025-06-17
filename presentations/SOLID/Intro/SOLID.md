## SOLID Principles  
### Clean Design for Maintainable Code

> "SOLID is about writing code that’s easy to change and hard to break."

--

## SOLID in Summary

- **S** – One responsibility per module  
- **O** – Extend behavior without breaking existing code  
- **L** – Substitutes should behave like their parents  
- **I** – Don't force dependencies on unused behavior  
- **D** – Rely on interfaces, not concrete implementations


---

### S – Single Responsibility Principle (SRP) 🧩

**"A class should have only one reason to change."**  
— Robert C. Martin

> **Summary:** Every module or class should have just one scope.

--

**Example:**  
A chef cooks, a cashier handles payments. If one person tries to do both, mistakes happen and responsibilities become tangled.

---


### O – Open/Closed Principle (OCP) 🔓

**"Modules should be open for extension, but closed for modification."**  
— Bertrand Meyer

> **Summary:** You should be able to add new behavior without altering existing code.

--

**Example:**  
Think of adding a new USB device to your computer — the operating system allows new devices without rewriting its core logic.

---


### L – Liskov Substitution Principle (LSP) 🔁

**"If it looks like a duck, swims like a duck, and quacks like a duck, then it probably is a duck."**

> **Summary:** Subtypes must be usable anywhere their base types are expected.

--

**Example:**  
If a driver can use any vehicle — car, truck, or electric scooter — they shouldn’t need to know how each one works differently to drive them.

---


### I – Interface Segregation Principle (ISP) 🎚️

**"Clients should not be forced to depend on methods they do not use."**  
— Robert C. Martin

> **Summary:** Prefer multiple small interfaces over a single large one.

--

**Example:**  
A basic TV remote shouldn't require buttons for smart features if the user only wants to turn the TV on and off.

---


### D – Dependency Inversion Principle (DIP) 🔌

**"Depend on abstractions, not on concretions."**  
— Robert C. Martin

> **Summary:** High-level code shouldn't rely on details; both should depend on abstractions.

--

**Example:**  
A hotel plug adapter lets any appliance connect to any socket — you don't need to change the appliance or the wall socket.
