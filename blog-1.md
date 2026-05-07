# `any` vs `unknown` in TypeScript

---

## 🔴 `any` — The Type Safety Hole

### What is `any`?
`any` is a special TypeScript type that completely **opts out of type checking**. When you assign `any` to a variable, TypeScript stops analyzing it — it can hold literally anything and be used in any way without complaint.

### What data can it hold?
Anything — primitives, objects, arrays, functions, `null`, `undefined`. No restrictions whatsoever.

```ts
// Primitives
let x: any = 42;
x = "hello";
x = true;
x = null;

// Non-primitives
x = { name: "Oli" };
x = [1, 2, 3];
x = () => console.log("I'm a function");
```

### Simple Example

```ts
let data: any = "hello";

console.log(data.toUpperCase());  // ✅ works — "HELLO"

data = 99;
console.log(data.toUpperCase());  // 💥 Runtime crash! Numbers have no toUpperCase()
// TypeScript said NOTHING. No warning. No error.
```

### Drawbacks of `any`
- TypeScript **fully trusts you** and checks nothing
- Errors only surface at **runtime**, not compile time
- Defeats the entire purpose of using TypeScript
- Spreads silently — once a variable is `any`, anything that touches it becomes unsafe too
- No IDE autocomplete or safety guarantees

---

## 🟢 `unknown` — The Safe Alternative

### What is `unknown`?
`unknown` is TypeScript's **type-safe counterpart to `any`**. It also accepts any value — but unlike `any`, TypeScript **refuses to let you use it** until you first prove what type it actually is. It forces you to be responsible.

### What data can it hold?
Same as `any` — primitives, objects, arrays, functions, `null`, `undefined`. The difference is in **what you can do with it**, not what it stores.

```ts
// Primitives
let y: unknown = 42;
y = "hello";
y = true;
y = null;

// Non-primitives
y = { name: "Oli" };
y = [1, 2, 3];
y = () => {};
```

### Simple Example

```ts
let data: unknown = "hello";

// ❌ TypeScript BLOCKS this immediately at compile time:
console.log(data.toUpperCase()); // Error: Object is of type 'unknown'

// ✅ You must narrow the type first:
if (typeof data === "string") {
  console.log(data.toUpperCase()); // Safe! TypeScript now knows it's a string
}
```

### Drawbacks of `unknown`
- Requires extra code (narrowing checks) before use
- Slightly more verbose than `any`
- Can feel annoying for quick prototyping

---

## 🔍 Type Narrowing — The Bridge

### What is it?
Type narrowing is the process of **moving from a broad/uncertain type to a specific one** through runtime checks. TypeScript watches your conditions and automatically narrows the type inside those blocks.

### Common Narrowing Techniques

```ts
function process(value: unknown) {

  // 1. typeof — for primitives
  if (typeof value === "string") {
    console.log(value.toUpperCase()); // TypeScript knows: string ✅
  }

  // 2. typeof — for numbers
  if (typeof value === "number") {
    console.log(value.toFixed(2));    // TypeScript knows: number ✅
  }

  // 3. Array.isArray — for arrays
  if (Array.isArray(value)) {
    console.log(value.length);        // TypeScript knows: array ✅
  }

  // 4. instanceof — for class instances
  if (value instanceof Date) {
    console.log(value.getFullYear()); // TypeScript knows: Date ✅
  }

  // 5. typeof object check — for plain objects
  if (typeof value === "object" && value !== null) {
    console.log(value);               // TypeScript knows: object (not null) ✅
  }
}
```

---

## ⚖️ Side-by-Side Comparison

| Feature | `any` | `unknown` |
|---|---|---|
| Accepts all values | ✅ | ✅ |
| Requires type check before use | ❌ No | ✅ Yes |
| TypeScript checks it | ❌ Never | ✅ Always |
| Runtime crash risk | 🔴 High | 🟢 Low |
| Use case | Legacy code, quick hacks | API responses, user input, external data |

---

## ✅ Golden Rule

> Use `any` → you're **telling** TypeScript *"trust me, I know what this is"* — even when you don't.
>
> Use `unknown` → you're **telling** TypeScript *"I don't know yet — I'll prove it before I use it"* — which is always the honest, safer choice.
