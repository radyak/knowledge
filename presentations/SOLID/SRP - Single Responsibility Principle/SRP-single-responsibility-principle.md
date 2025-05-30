## Single Responsibility Principle
### The "S" in SOLID

---

<!-- .slide: data-transition="fade" -->
## Single Responsibility Principle (SRP)

<img style="width: 300px; float: left" src="https://upload.wikimedia.org/wikipedia/commons/2/27/Robert_C._Martin_surrounded_by_computers.jpg">

_"A class should have only one reason to change."_  
— Robert C. Martin, *Clean Architecture*

> "A class should have only one reason to change."
> 
> — Robert C. Martin, *Clean Code*

---

<!-- .slide: data-transition="fade" -->
## Synonymous Phrases

- **One job per class**
- **Do one thing and do it well**
- **High cohesion, low responsibility scope**
- **Separation of concerns**
- **"Single reason to change"**

---

## What Does It Mean?

- **One job per class** 📋
- **Single focus** 🎯
- **Clear purpose** ✨
- **Minimal coupling** 🔗

---

<!-- .slide: data-transition="fade" -->
## Real-World Analogy

**A chef vs. a restaurant manager**

- A chef is responsible for cooking — one clear responsibility.
- A manager handles staffing, logistics, customer service.
- Mixing both in one role causes confusion and inefficiency.

**➡ Split responsibilities to increase clarity and adaptability.**

---


## Real-World Example 🏪

**Bad:** A Swiss Army Knife Employee
- Cashier who also stocks shelves
- Also handles customer complaints
- Also manages inventory
- Also cleans the store

**Good:** Specialized Roles
- **Cashier:** Only handles transactions
- **Stocker:** Only manages inventory
- **Customer Service:** Only handles complaints
- **Janitor:** Only maintains cleanliness

---

## Code Example: The Problem ❌

```javascript
class UserManager {
  constructor() {
    this.users = [];
  }

  // User management
  addUser(user) { this.users.push(user); }
  removeUser(id) { /* remove user logic */ }
  
  // Email functionality
  sendWelcomeEmail(user) {
    console.log(`Sending email to ${user.email}`);
    // Email sending logic...
  }
  
  // Database operations
  saveToDatabase() {
    console.log('Saving users to database...');
    // Database logic...
  }
  
  // Logging
  logUserActivity(action, user) {
    console.log(`${action}: ${user.name}`);
    // Logging logic...
  }
}
```

**Problems:** Too many responsibilities! 😵

---

## Code Example: The Solution ✅

```javascript
// Single responsibility: User data management
class UserRepository {
  constructor() { this.users = []; }
  
  addUser(user) { this.users.push(user); }
  removeUser(id) { /* remove user logic */ }
  getAllUsers() { return this.users; }
}

// Single responsibility: Email operations
class EmailService {
  sendWelcomeEmail(user) {
    console.log(`Sending email to ${user.email}`);
    // Email sending logic...
  }
}

// Single responsibility: Database operations
class DatabaseService {
  saveUsers(users) {
    console.log('Saving users to database...');
    // Database logic...
  }
}

// Single responsibility: Activity logging
class ActivityLogger {
  logUserActivity(action, user) {
    console.log(`${action}: ${user.name}`);
    // Logging logic...
  }
}
```

---

<!-- .slide: data-transition="fade" -->
## Code Example – Violating SRP

```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate(self):
        # create report
        pass

    def save_to_file(self, filename):
        # violates SRP — persistence logic included
        with open(filename, 'w') as f:
            f.write(self.generate())
```

---

<!-- .slide: data-transition="fade" -->

## Code Example – Respecting SRP

```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate(self):
        # only generates report content
        return "Report content"

class ReportSaver:
    def save(self, report, filename):
        with open(filename, 'w') as f:
            f.write(report.generate())

```
Each class now has only one reason to change.

---

## Benefits of SRP 🎉

- **Easier to understand** 🧠
- **Easier to test** 🧪
- **Easier to maintain** 🔧
- **Reduced coupling** 🔗
- **Better reusability** ♻️
- **Cleaner architecture** 🏗️

---

<!-- .slide: data-transition="fade" -->
## Daily Practice Tips

    ✅ Name classes and methods after a single, clear purpose

    ✅ Extract unrelated behavior into separate classes or modules

    ✅ Regularly ask: Why would this class need to change?

    ✅ Use unit tests to spot violations (too many responsibilities make testing hard)

    ✅ Refactor when responsibilities grow over time

---

## Daily Practice Tips 💡

### 1. Ask the Right Questions
- What is this class responsible for?
- How many reasons could it change?
- Can I describe it in one sentence?

### 2. Watch for Warning Signs
- Classes with "And" in their name
- Methods that don't relate to each other
- Multiple import statements for unrelated libraries

---

## Daily Practice Tips (Continued) 💡

### 3. Use the "One Sentence Rule"
If you can't describe a class's purpose in one clear sentence, it probably violates SRP.

### 4. Follow the "No More Than 7±2" Rule
- Limit methods per class
- Keep classes focused and small

### 5. Regular Refactoring
- Extract methods and classes regularly
- Look for opportunities to separate concerns

---

## Common Anti-Patterns to Avoid ⚠️

- **God Classes** - Classes that do everything
- **Utility Classes** - Catch-all static method containers
- **Manager Classes** - Vague responsibilities
- **Mixed Concerns** - UI logic mixed with business logic

---

## Quick Checklist ✓

Before committing code, ask:

- [ ] Does this class have a single, clear purpose?
- [ ] Would changes to different features require modifying this class?
- [ ] Can I easily write unit tests for this class?
- [ ] Would a new developer understand this class quickly?
- [ ] Is the class name specific and descriptive?

---

## Remember the Bee! 🐝

Just like a worker bee has **one job** - collecting nectar - each class should have **one responsibility**.

*Focus, simplicity, and clarity lead to maintainable code.*

---

<!-- .slide: data-transition="fade" -->
## Final Thoughts

> "SRP is about people — when two people need to change the same class for different reasons, SRP is violated."
>   — Robert C. Martin

Keep your code clean, focused, and maintainable.