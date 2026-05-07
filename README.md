# Assignment 01 — Problem Solving with TypeScript & OOP

## 📋 Overview
This assignment covers fundamental TypeScript concepts including type safety, generics, interfaces, class inheritance, and OOP principles through practical problem solving.

---

## 🔗 Live Links
- 🖥️ **GitHub Repo:** [https://github.com/mohammad-oli56/L-2-assingment01](#)

---

## 📁 Project Structure

```
├── solutions.ts        # All 7 problem solutions
├── blog-1.md           #any vs unknown in TypeScript
├── blog-2.md           # The Four Pillars of OOP in TypeScript
└── README.md           # Assignment documentation
```

---

## 💻 Problems Solved

| # | Problem | Concept Used |
|---|---|---|
| 1 | `filterEvenNumbers` | Array filter, typed parameter |
| 2 | `reverseString` | String manipulation |
| 3 | `checkType` | Union type, type guard |
| 4 | `getProperty` | Generics with `keyof` constraint |
| 5 | `toggleReadStatus` | Interface, intersection type |
| 6 | `Person` / `Student` | OOP — class, extends, super() |
| 7 | `getIntersection` | Set for O(n) intersection |

---

## 🧠 Key Concepts Explained

### 1. Why `unknown` is safer than `any`
- `any` completely opts out of type checking — TypeScript trusts you blindly, errors only appear at **runtime**
- `unknown` forces you to **prove the type first** (via type narrowing) before using the value
- Type narrowing uses `typeof`, `instanceof`, or `Array.isArray()` to safely narrow `unknown` into a specific type

### 2. The Four Pillars of OOP in TypeScript

| Pillar | What it does |
|---|---|
| **Inheritance** | Child class reuses parent's code — avoids repetition |
| **Polymorphism** | Same method name, different behavior per class |
| **Abstraction** | Hides internal complexity, exposes only what's needed |
| **Encapsulation** | Locks internal data with `private`/`protected` — prevents corruption |

---

## 🚀 How to Run

```bash
# Compile TypeScript
tsc solutions.ts

# Run compiled JavaScript
node solutions.js or node ./solutions.js 
```

---

## 👤 Author
**Oli** [https://github.com/mohammad-oli56](#)
