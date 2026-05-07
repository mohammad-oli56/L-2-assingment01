# The Four Pillars of OOP in TypeScript

---

## 1. 🧬 Inheritance

### What is it?
Inheritance allows a class to **acquire properties and methods of another class**. The child class gets everything from the parent and can also add its own on top.

### Why use it?
Instead of rewriting the same code in multiple classes, you write it **once in a parent** and all children automatically get it. Reduces repetition.

### Example

```ts
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  move(): void {
    console.log(`${this.name} is moving`);
  }
}

class Dog extends Animal {
  bark(): void {
    console.log(`${this.name} says: Woof!`);
  }
}

const dog = new Dog("Bruno");
dog.move();  // ✅ inherited from Animal → "Bruno is moving"
dog.bark();  // ✅ Dog's own method   → "Bruno says: Woof!"
```

---

## 2. 🎭 Polymorphism

### What is it?
Polymorphism means **one interface, many forms**. The same method name behaves differently depending on which class is calling it.

### Why use it?
You can call the **same method on different objects** and each one responds in its own way — without writing separate logic for each type.

### Example

```ts
class Shape {
  area(): number {
    return 0;
  }
}

class Circle extends Shape {
  constructor(private radius: number) { super(); }
  area(): number {
    return Math.PI * this.radius ** 2; // Circle's own formula
  }
}

class Rectangle extends Shape {
  constructor(private width: number, private height: number) { super(); }
  area(): number {
    return this.width * this.height; // Rectangle's own formula
  }
}

const shapes: Shape[] = [new Circle(5), new Rectangle(4, 6)];

shapes.forEach(shape => {
  console.log(shape.area()); // ✅ Same method call, different result each time
});
// 78.53...
// 24
```

---

## 3. 🎭 Abstraction

### What is it?
Abstraction means **hiding complex internal details** and only exposing what is necessary. You show *what* something does, not *how* it does it.

### Why use it?
Users of your class don't need to know the internal logic — they just call the method and trust it works. Keeps things **simple and clean from the outside**.

### Example

```ts
abstract class Database {
  // Abstract method — child MUST implement this
  abstract connect(): void;

  // Shared method — already implemented
  logStatus(): void {
    console.log("Checking connection status...");
    this.connect();
  }
}

class MongoDB extends Database {
  connect(): void {
    console.log("MongoDB connected!"); // internal detail hidden here
  }
}

class MySQL extends Database {
  connect(): void {
    console.log("MySQL connected!"); // internal detail hidden here
  }
}

const db1 = new MongoDB();
db1.logStatus(); // User just calls logStatus — doesn't care HOW it connects
// "Checking connection status..."
// "MongoDB connected!"
```

---

## 4. 🔒 Encapsulation

### What is it?
Encapsulation means **bundling data and methods together** inside a class, and **restricting direct access** to internal data using access modifiers (`private`, `protected`, `public`).

### Why use it?
Prevents outside code from accidentally **breaking internal state**. You control exactly what gets read or changed, and how.

### Example

```ts
class BankAccount {
  private balance: number = 0; // ❌ Cannot be touched directly from outside

  deposit(amount: number): void {
    if (amount > 0) this.balance += amount; // ✅ Controlled way to change balance
  }

  withdraw(amount: number): void {
    if (amount <= this.balance) this.balance -= amount;
    else console.log("Insufficient funds!");
  }

  getBalance(): number {
    return this.balance; // ✅ Controlled way to read balance
  }
}

const account = new BankAccount();
account.deposit(500);
account.withdraw(200);
console.log(account.getBalance()); // ✅ 300

// account.balance = 99999; // 💥 Error! Private — blocked by TypeScript
```

---

## ⚖️ All Four Pillars — Quick Reference

| Pillar | One Line Definition | Main Benefit |
|---|---|---|
| **Inheritance** | Child class gets parent's code | Avoid repetition |
| **Polymorphism** | Same method, different behavior | Flexible, interchangeable objects |
| **Abstraction** | Hide complexity, show only what's needed | Cleaner, simpler interface |
| **Encapsulation** | Lock internal data, control access | Prevents accidental data corruption |

---

## ✅ Why All Four Matter in Large Projects

> In a large TypeScript project with hundreds of classes and thousands of lines —
> **Inheritance** stops you from copy-pasting logic everywhere,
> **Polymorphism** lets you swap components without rewriting logic,
> **Abstraction** keeps each class's surface area small and understandable,
> and **Encapsulation** ensures no part of the system can silently corrupt another's data.
>
> Together, they turn a chaotic codebase into a **structured, maintainable system**.
