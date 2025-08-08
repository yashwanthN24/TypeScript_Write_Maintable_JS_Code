# TypeScript Cheatsheet: Write Maintainable JS Code

## Introduction

* **TypeScript** is JavaScript with types.
* It is a **superset** of JavaScript.
* Offers **type safety**, static typing, and better code maintainability.
* Built to write **robust, scalable** applications.

---

### TypeScript vs JavaScript

* JS is dynamic and loosely typed.
* TypeScript provides **compile-time error checking**.
* Similar to statically typed languages like C++, Java, and C#.

> "Static typing" helps detect bugs early.

---

## Setup

1. Install Node.js (LTS)
2. Install TypeScript:

```bash
npm install -g typescript
```

3. Verify:

```bash
tsc -v
```

4. Project setup:

```bash
mkdir src
cd src
tsc --init
```

---

## Types in TypeScript

### Basic Types

* number
* string
* boolean
* null / undefined
* object

### Extended Types

* `any` (avoid this)
* `unknown`
* `never`
* `enum`
* `tuple`

### Type Annotations

```ts
let username: string;
```

---

## Functions

* Typed parameters and return types

```ts
function greet(name: string): string {
  return `Hello ${name}`;
}
```

* Optional / Default / Rest Params
* Arrow and Anonymous functions
* `void` and `never` types

---

## Advanced Types

* Union: `type A = string | number`
* Literal: `let mode: 'light' | 'dark'`
* Nullable: `string | null`
* Type Alias:

```ts
type User = { id: number, name: string }
```

* Intersection: `type Full = A & B`

---

## Arrays and Tuples

### Arrays

```ts
let nums: number[] = [1, 2, 3];
```

### Multi-dimensional Arrays

```ts
let matrix: number[][] = [[1], [2]];
```

### Tuples

```ts
let user: [string, number] = ["Yash", 23];
```

---

## Enums

```ts
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT"
}
```

---

## Interfaces

### Basic

```ts
interface User {
  id: number;
  name: string;
}
```

### Interface Reopening

```ts
interface User {
  email: string;
}
```

### Use Cases

* Modular development
* Backward compatibility
* Clear structure

---

## Classes

### Class Declaration

```ts
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

### Access Modifiers

* `public` (default)
* `private`
* `protected`

### Accessors

```ts
class Counter {
  private _value = 0;

  get value() {
    return this._value;
  }
  set value(val: number) {
    this._value = val;
  }
}
```

### Static Members

```ts
class MathUtil {
  static PI = 3.14;
}
```

### Abstract Classes

```ts
abstract class Shape {
  abstract area(): number;
}

class Circle extends Shape {
  constructor(private r: number) { super(); }
  area() { return Math.PI * this.r ** 2; }
}
```

---

## Type Assertion

```ts
let someValue: unknown = "Hello World";
let strLength = (someValue as string).length;
```

---

# GENERICS

## 1. What are Generics?

* Allows functions/classes to work with **any data type**.
* Maintains **type safety**.

```ts
function identity<T>(arg: T): T {
  return arg;
}

const output = identity<string>("Hello");
```

## 2. Generics with Multiple Types

```ts
function merge<T, U>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const result = merge({ name: "Yash" }, { age: 23 });
```

## 3. Generic Classes

```ts
class Box<T> {
  content: T;
  constructor(value: T) {
    this.content = value;
  }
}

const stringBox = new Box<string>("TypeScript");
```

## 4. Generics with Interfaces

```ts
interface ApiResponse<T> {
  data: T;
  error?: string;
}

const response: ApiResponse<string> = {
  data: "Success"
};
```

## 5. Type Assertions

```ts
let data: unknown = "test";
let str = (data as string).toUpperCase();
```

---

# DECORATORS

## What are Decorators?

* A decorator is a **special kind of declaration** that can be attached to a class, method, accessor, property, or parameter.
* It’s a **meta-programming feature**.

### Syntax

```ts
function Logger(constructor: Function) {
  console.log("Logging...", constructor.name);
}

@Logger
class User {
  constructor(public name: string) {}
}
```

### Why Use Decorators Instead of Functions?

* Decorators add behavior **at design/definition time**, not just at execution.
* Clean separation of concerns (e.g., logging, validation, access control).
* Works well with frameworks (like NestJS, Angular).
* Avoids polluting business logic with boilerplate.

### Native JS vs TypeScript Decorators

| Feature        | Native JS                 | TypeScript Decorators      |
| -------------- | ------------------------- | -------------------------- |
| Support        | Proposal stage (2024+)    | Fully supported with flag  |
| Usage          | Manual behavior injection | Auto-wired, elegant syntax |
| Real-world Use | Limited                   | Widely used in NestJS etc. |

> To enable decorators in TypeScript, use this in `tsconfig.json`:

```json
"experimentalDecorators": true
```

### Example: Method Decorator

```ts
function Log(target: any, name: string, descriptor: PropertyDescriptor) {
  const original = descriptor.value;
  descriptor.value = function (...args: any[]) {
    console.log(`Called ${name} with`, args);
    return original.apply(this, args);
  };
}

class Calculator {
  @Log
  add(a: number, b: number) {
    return a + b;
  }
}
```

### Example: Class Decorator with Metadata

```ts
function Sealed(constructor: Function) {
  Object.seal(constructor);
  Object.seal(constructor.prototype);
}

@Sealed
class Vehicle {
  constructor(public model: string) {}
}
```

---

## Images (Original as requested)

![image](https://github.com/user-attachments/assets/7c199f4c-e8ab-4ba2-93d9-d2712cc2b438)

![image](https://github.com/user-attachments/assets/6863a2a9-7c7c-4790-9974-32e6c998bfcc)

![image](https://github.com/user-attachments/assets/0f471703-2ef7-4c56-a536-ebc038dcf351)

... *(and all other provided images in the same order you shared)* ...

---

## Summary

TypeScript enhances JavaScript by enforcing types at compile time. Key takeaways:

* Use `tsc --init` to get started
* Write robust, maintainable apps
* Embrace generics, interfaces, decorators, and classes for scalable code

---

Let me know if you want this exported to **PDF/Notion/Markdown file** or want quizzes added for each section.
