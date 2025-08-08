# Complete TypeScript Guide
*A comprehensive resource for writing maintainable JavaScript code with TypeScript*

## Table of Contents
1. [Introduction to TypeScript](#introduction-to-typescript)
2. [Setup and Installation](#setup-and-installation)
3. [Basic Types](#basic-types)
4. [Functions](#functions)
5. [Advanced Types](#advanced-types)
6. [Arrays and Tuples](#arrays-and-tuples)
7. [Enums](#enums)
8. [Interfaces](#interfaces)
9. [Classes](#classes)
10. [Type Assertions](#type-assertions)
11. [Generics](#generics)

---

## Introduction to TypeScript

### What is TypeScript?
- **TypeScript is JavaScript with syntax for types**
- A superset of JavaScript that helps write better and maintainable JS code
- All about type safety and static typing
- A programming language built on top of JavaScript
- Enhances JavaScript by offering features that aid in creating robust applications
- Reduces development time through compile-time error checking

### Key Features
- **Static Typing**: The most significant feature TypeScript provides
- **Compile-time Error Checking**: Catches errors before runtime
- **Enhanced IDE Support**: Better autocomplete, refactoring, and navigation
- **Modern JavaScript Features**: Support for latest ECMAScript features

### Why Learn TypeScript?

#### Benefits
- ✅ **High Industry Demand**: Widely adopted in enterprise applications
- ✅ **Code Simplification**: Makes JavaScript code more readable and maintainable
- ✅ **Efficiency**: Faster development with better tooling
- ✅ **Error Prevention**: Detects errors before runtime
- ✅ **Quick Feedback**: Instant feedback during development
- ✅ **Framework Empowerment**: Better integration with modern frameworks

### How TypeScript Works
```
TypeScript Code (.ts) → TypeScript Compiler (tsc) → JavaScript Code (.js)
```
This process is called **Transpilation** - converting TypeScript to JavaScript.

---

## Setup and Installation

### Prerequisites
1. **Visual Studio Code** - Recommended IDE
2. **Node.js (LTS)** - Runtime environment

### Installation Steps
```bash
# Verify Node.js installation
node --version

# Install TypeScript globally
npm install -g typescript

# Verify TypeScript installation
tsc --version
```

### Project Setup
```bash
# Create project structure
mkdir my-typescript-project
cd my-typescript-project
mkdir src

# Create TypeScript config file
tsc --init

# Create your first TypeScript file
touch src/index.ts
```

### tsconfig.json
The `tsconfig.json` file contains compilation options that the TypeScript compiler uses.

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true
  }
}
```

---

## Basic Types

### Primitive Types
TypeScript extends JavaScript's built-in types and adds new ones:

```typescript
// JavaScript built-in types
let name: string = "John";
let age: number = 25;
let isActive: boolean = true;
let data: null = null;
let notDefined: undefined = undefined;

// TypeScript additional types
let anything: any = "can be anything";
let unknownValue: unknown = "safer than any";
let neverReturns: never; // Function that never returns
```

### Type Annotations
Explicitly specify the type of variables, functions, or entities using a colon (:) followed by the type.

```typescript
// Variable type annotations
let userName: string = "Alice";
let userAge: number = 30;
let isLoggedIn: boolean = false;

// Function parameter and return type annotations
function greet(name: string): string {
  return `Hello, ${name}!`;
}

// Multiple variable declaration
let firstName: string, lastName: string, fullName: string;
```

### The 'any' Type
```typescript
let dynamicValue: any = 42;
dynamicValue = "Now it's a string";
dynamicValue = { name: "Now it's an object" };

// ⚠️ Avoid using 'any' as it disables TypeScript's type checking
```

### Object Type Annotations
Specify the types of properties that an object must have:

```typescript
// Object type annotation
let person: {
  name: string;
  age: number;
  isEmployed: boolean;
} = {
  name: "John Doe",
  age: 30,
  isEmployed: true
};

// Optional properties
let user: {
  name: string;
  email?: string; // Optional property
} = {
  name: "Jane"
};
```

---

## Functions

### Function Type Annotations
```typescript
// Function declaration with types
function add(a: number, b: number): number {
  return a + b;
}

// Function expression
const multiply = function(x: number, y: number): number {
  return x * y;
};
```

### Optional and Default Parameters
```typescript
// Optional parameters (use ?)
function greetUser(name: string, age?: number): string {
  if (age) {
    return `Hello ${name}, you are ${age} years old`;
  }
  return `Hello ${name}`;
}

// Default parameters
function createUser(name: string, role: string = "user"): object {
  return { name, role };
}
```

### Rest Parameters
```typescript
function sum(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}

// Usage
console.log(sum(1, 2, 3, 4, 5)); // 15
```

### Arrow Functions
```typescript
// Arrow function with explicit types
const divide = (a: number, b: number): number => {
  return a / b;
};

// Shortened arrow function
const square = (x: number): number => x * x;

// Arrow function with object return
const createPerson = (name: string, age: number): {name: string, age: number} => ({
  name,
  age
});
```

### Anonymous Functions
```typescript
// Anonymous function in array method
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(function(num: number): number {
  return num * 2;
});

// Anonymous function as callback
setTimeout(function(): void {
  console.log("Timer expired");
}, 1000);
```

### void and never Types
```typescript
// void - function doesn't return a value
function logMessage(message: string): void {
  console.log(message);
  // No return statement or return undefined
}

// never - function never returns (throws error or infinite loop)
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {
    // This function never terminates
  }
}
```

---

## Advanced Types

### Union Types
Allow a variable to be one of several types:

```typescript
// Union type
let id: string | number;
id = "ABC123";  // Valid
id = 123;       // Valid

// Function with union parameter
function formatId(id: string | number): string {
  if (typeof id === "string") {
    return id.toUpperCase();
  }
  return id.toString();
}

// Union with multiple types
let status: "loading" | "success" | "error" = "loading";
```

### Literal Types
Exact values that a variable can have:

```typescript
// String literal types
let direction: "north" | "south" | "east" | "west";
direction = "north"; // Valid
// direction = "up"; // Error

// Numeric literal types
let diceRoll: 1 | 2 | 3 | 4 | 5 | 6;

// Boolean literal types
let isComplete: true = true;

// Combined with union types
type Status = "idle" | "loading" | "success" | "error";
let currentStatus: Status = "idle";
```

### Nullable Types
```typescript
// Nullable types (union with null/undefined)
let userName: string | null = null;
let userAge: number | undefined = undefined;

// Function that might return null
function findUser(id: number): User | null {
  // Return user or null if not found
  return users.find(user => user.id === id) || null;
}

// Optional chaining with nullable types
let user: {name?: string} | null = getUser();
console.log(user?.name?.toUpperCase());
```

### Type Aliases
Create custom names for types:

```typescript
// Basic type alias
type StringOrNumber = string | number;
type UserID = string | number;

// Object type alias
type User = {
  id: UserID;
  name: string;
  email: string;
  isActive: boolean;
};

// Function type alias
type EventHandler = (event: string) => void;

// Generic type alias
type ApiResponse<T> = {
  data: T;
  status: number;
  message: string;
};

// Usage
const user: User = {
  id: "123",
  name: "John",
  email: "john@email.com",
  isActive: true
};
```

### Intersection Types
Combine multiple types into one:

```typescript
// Basic intersection
type Person = {
  name: string;
  age: number;
};

type Employee = {
  employeeId: string;
  department: string;
};

// Intersection type
type Staff = Person & Employee;

const employee: Staff = {
  name: "Alice",
  age: 30,
  employeeId: "EMP001",
  department: "Engineering"
};

// Intersection with methods
type Flyable = {
  fly(): void;
};

type Swimmable = {
  swim(): void;
};

type FlyingFish = Flyable & Swimmable;

const flyingFish: FlyingFish = {
  fly() { console.log("Flying!"); },
  swim() { console.log("Swimming!"); }
};
```

---

## Arrays and Tuples

### Array Type Annotations
```typescript
// Array of strings
let fruits: string[] = ["apple", "banana", "orange"];

// Alternative syntax
let numbers: Array<number> = [1, 2, 3, 4, 5];

// Array of objects
let users: {name: string, age: number}[] = [
  { name: "John", age: 25 },
  { name: "Jane", age: 30 }
];

// Union type arrays
let mixedArray: (string | number)[] = ["hello", 42, "world", 100];

// Read-only arrays
let readOnlyNumbers: readonly number[] = [1, 2, 3];
// readOnlyNumbers.push(4); // Error: Property 'push' does not exist
```

### Multidimensional Arrays
```typescript
// 2D array
let matrix: number[][] = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

// 3D array
let cube: number[][][] = [
  [[1, 2], [3, 4]],
  [[5, 6], [7, 8]]
];

// Array of string arrays
let wordLists: string[][] = [
  ["apple", "banana"],
  ["car", "bike"],
  ["red", "blue"]
];
```

### Tuples
Fixed-length arrays with specific types at each position:

```typescript
// Basic tuple
let person: [string, number] = ["John", 25];
let coordinates: [number, number] = [10, 20];

// Accessing tuple elements
console.log(person[0]); // "John"
console.log(person[1]); // 25

// Tuple with different types
let userInfo: [string, number, boolean] = ["Alice", 30, true];

// Optional tuple elements
let optionalTuple: [string, number?] = ["test"];

// Rest elements in tuples
let restTuple: [string, ...number[]] = ["first", 1, 2, 3, 4];

// Named tuples (TypeScript 4.0+)
let namedTuple: [name: string, age: number] = ["Bob", 35];

// Read-only tuples
let readOnlyTuple: readonly [string, number] = ["immutable", 42];
```

---

## Enums

Enums define a set of named constant values representing discrete options:

### Numeric Enums
```typescript
// Basic numeric enum (starts from 0)
enum Direction {
  Up,     // 0
  Down,   // 1
  Left,   // 2
  Right   // 3
}

// Custom numeric values
enum StatusCode {
  Success = 200,
  NotFound = 404,
  InternalError = 500
}

// Mixed numeric enum
enum MixedEnum {
  First = 1,
  Second,      // 2 (auto-increment)
  Third = 10,
  Fourth       // 11 (auto-increment)
}

// Usage
let currentDirection: Direction = Direction.Up;
console.log(currentDirection); // 0
console.log(Direction[0]); // "Up" (reverse mapping)
```

### String Enums
```typescript
// String enum
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT"
}

enum Theme {
  Light = "light",
  Dark = "dark",
  Auto = "auto"
}

// Usage
let userTheme: Theme = Theme.Dark;
console.log(userTheme); // "dark"

// No reverse mapping for string enums
// console.log(Theme["dark"]); // Error
```

### Heterogeneous Enums
```typescript
// Mixed string and numeric enum (not recommended)
enum MixedEnum {
  No = 0,
  Yes = "YES"
}
```

### Const Enums
```typescript
// Const enum (inlined at compile time)
const enum Colors {
  Red = "red",
  Green = "green",
  Blue = "blue"
}

let color = Colors.Red; // Becomes let color = "red";
```

---

## Interfaces

Interfaces define the shape of objects and contracts for classes:

### Basic Interface
```typescript
// Interface definition
interface User {
  id: number;
  name: string;
  email: string;
  isActive: boolean;
}

// Using the interface
const user: User = {
  id: 1,
  name: "John Doe",
  email: "john@example.com",
  isActive: true
};

// Function using interface
function createUser(userData: User): User {
  return { ...userData };
}
```

### Optional Properties
```typescript
interface Product {
  id: number;
  name: string;
  description?: string;  // Optional
  price: number;
  category?: string;     // Optional
}

const product: Product = {
  id: 1,
  name: "Laptop",
  price: 999.99
  // description and category are optional
};
```

### Readonly Properties
```typescript
interface Config {
  readonly apiUrl: string;
  readonly version: number;
  timeout?: number;
}

const config: Config = {
  apiUrl: "https://api.example.com",
  version: 1,
  timeout: 5000
};

// config.apiUrl = "new-url"; // Error: Cannot assign to readonly property
```

### Method Signatures
```typescript
interface Calculator {
  add(a: number, b: number): number;
  subtract(a: number, b: number): number;
  multiply?(a: number, b: number): number; // Optional method
}

const calc: Calculator = {
  add(a, b) { return a + b; },
  subtract(a, b) { return a - b; }
  // multiply is optional, so it can be omitted
};
```

### Interface Extension
```typescript
// Base interface
interface Animal {
  name: string;
  age: number;
}

// Extended interface
interface Dog extends Animal {
  breed: string;
  bark(): void;
}

// Multiple inheritance
interface Pet {
  owner: string;
}

interface DomesticDog extends Dog, Pet {
  isVaccinated: boolean;
}

const myDog: DomesticDog = {
  name: "Buddy",
  age: 3,
  breed: "Golden Retriever",
  owner: "John",
  isVaccinated: true,
  bark() { console.log("Woof!"); }
};
```

### Interface Reopening (Declaration Merging)
```typescript
// First declaration
interface User {
  name: string;
}

// Second declaration - merged with first
interface User {
  email: string;
}

// Third declaration - adds more properties
interface User {
  age?: number;
}

// Now User has name, email, and age
const user: User = {
  name: "John",
  email: "john@example.com",
  age: 30
};
```

### Built-in Interfaces
TypeScript provides built-in interfaces for HTML elements:

```typescript
// HTML Element interfaces
const button: HTMLButtonElement = document.createElement('button');
const input: HTMLInputElement = document.createElement('input');
const div: HTMLDivElement = document.createElement('div');

// Event interfaces
function handleClick(event: MouseEvent): void {
  console.log('Clicked at:', event.clientX, event.clientY);
}

function handleKeyPress(event: KeyboardEvent): void {
  console.log('Key pressed:', event.key);
}
```

### Interfaces vs Type Aliases
```typescript
// Interface - can be extended and reopened
interface UserInterface {
  name: string;
}

interface UserInterface {
  email: string; // Declaration merging works
}

// Type alias - cannot be reopened
type UserType = {
  name: string;
};

// type UserType = { // Error: Duplicate identifier
//   email: string;
// }

// Use interfaces for object shapes that might be extended
// Use type aliases for unions, primitives, computed types
```

---

## Classes

### Basic Class with Type Annotations
```typescript
class Person {
  // Property declarations with types
  name: string;
  age: number;
  email: string;

  // Constructor with typed parameters
  constructor(name: string, age: number, email: string) {
    this.name = name;
    this.age = age;
    this.email = email;
  }

  // Method with return type
  greet(): string {
    return `Hello, I'm ${this.name}`;
  }

  // Method with parameters
  celebrateBirthday(): void {
    this.age++;
    console.log(`Happy birthday! Now ${this.age} years old.`);
  }
}

// Creating instance
const person = new Person("John", 25, "john@example.com");
```

### Access Modifiers
```typescript
class BankAccount {
  public accountNumber: string;    // Accessible everywhere (default)
  private balance: number;         // Accessible only within class
  protected accountType: string;   // Accessible within class and subclasses

  constructor(accountNumber: string, initialBalance: number) {
    this.accountNumber = accountNumber;
    this.balance = initialBalance;
    this.accountType = "savings";
  }

  // Public method
  public getBalance(): number {
    return this.balance;
  }

  // Private method
  private validateTransaction(amount: number): boolean {
    return amount > 0 && amount <= this.balance;
  }

  // Protected method
  protected updateBalance(amount: number): void {
    this.balance += amount;
  }

  public withdraw(amount: number): boolean {
    if (this.validateTransaction(amount)) {
      this.updateBalance(-amount);
      return true;
    }
    return false;
  }
}

const account = new BankAccount("123456", 1000);
console.log(account.accountNumber); // OK
console.log(account.getBalance());  // OK
// console.log(account.balance);    // Error: private
```

### Class Accessors (Getters and Setters)
```typescript
class Temperature {
  private _celsius: number = 0;

  // Getter
  get celsius(): number {
    return this._celsius;
  }

  // Setter with validation
  set celsius(value: number) {
    if (value < -273.15) {
      throw new Error("Temperature cannot be below absolute zero");
    }
    this._celsius = value;
  }

  // Computed property
  get fahrenheit(): number {
    return (this._celsius * 9/5) + 32;
  }

  set fahrenheit(value: number) {
    this.celsius = (value - 32) * 5/9;
  }
}

const temp = new Temperature();
temp.celsius = 25;
console.log(temp.fahrenheit); // 77
temp.fahrenheit = 100;
console.log(temp.celsius);    // 37.77...
```

### Static Members
```typescript
class MathUtils {
  static PI: number = 3.14159;
  
  private constructor() {
    // Prevent instantiation
  }

  static calculateArea(radius: number): number {
    return MathUtils.PI * radius * radius;
  }

  static max(a: number, b: number): number {
    return a > b ? a : b;
  }
}

// Usage without creating instance
console.log(MathUtils.PI);                    // 3.14159
console.log(MathUtils.calculateArea(5));      // 78.53975
console.log(MathUtils.max(10, 20));           // 20

// const utils = new MathUtils(); // Error: Constructor is private
```

### Class Implementing Interface
```typescript
interface Flyable {
  speed: number;
  fly(): void;
}

interface Swimmable {
  swim(): void;
}

class Bird implements Flyable {
  speed: number;
  name: string;

  constructor(name: string, speed: number) {
    this.name = name;
    this.speed = speed;
  }

  fly(): void {
    console.log(`${this.name} is flying at ${this.speed} mph`);
  }
}

class Duck implements Flyable, Swimmable {
  speed: number;
  name: string;

  constructor(name: string, speed: number) {
    this.name = name;
    this.speed = speed;
  }

  fly(): void {
    console.log(`${this.name} is flying`);
  }

  swim(): void {
    console.log(`${this.name} is swimming`);
  }
}
```

### Abstract Classes and Members
```typescript
abstract class Shape {
  abstract name: string;

  // Concrete method
  displayInfo(): void {
    console.log(`This is a ${this.name}`);
  }

  // Abstract method - must be implemented by subclasses
  abstract calculateArea(): number;
  abstract calculatePerimeter(): number;
}

class Rectangle extends Shape {
  name: string = "Rectangle";
  width: number;
  height: number;

  constructor(width: number, height: number) {
    super();
    this.width = width;
    this.height = height;
  }

  calculateArea(): number {
    return this.width * this.height;
  }

  calculatePerimeter(): number {
    return 2 * (this.width + this.height);
  }
}

class Circle extends Shape {
  name: string = "Circle";
  radius: number;

  constructor(radius: number) {
    super();
    this.radius = radius;
  }

  calculateArea(): number {
    return Math.PI * this.radius * this.radius;
  }

  calculatePerimeter(): number {
    return 2 * Math.PI * this.radius;
  }
}

// const shape = new Shape(); // Error: Cannot create instance of abstract class
const rect = new Rectangle(10, 5);
const circle = new Circle(3);
```

### Polymorphism and Method Override
```typescript
class Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  makeSound(): void {
    console.log("Some generic animal sound");
  }

  move(): void {
    console.log(`${this.name} is moving`);
  }
}

class Dog extends Animal {
  breed: string;

  constructor(name: string, breed: string) {
    super(name); // Call parent constructor
    this.breed = breed;
  }

  // Override parent method
  makeSound(): void {
    console.log("Woof! Woof!");
  }

  // Additional method specific to Dog
  fetch(): void {
    console.log(`${this.name} is fetching the ball`);
  }
}

class Cat extends Animal {
  // Override parent method
  makeSound(): void {
    console.log("Meow! Meow!");
  }

  // Override parent method with additional behavior
  move(): void {
    console.log(`${this.name} is sneaking quietly`);
  }
}

// Polymorphism in action
const animals: Animal[] = [
  new Dog("Buddy", "Golden Retriever"),
  new Cat("Whiskers"),
  new Animal("Generic Pet")
];

animals.forEach(animal => {
  animal.makeSound(); // Calls the overridden method for each type
  animal.move();
});
```

### Class vs Interface Summary
- **Class**: For creating objects with implementation
- **Interface**: For defining the shape/contract of objects
- **Abstract Class**: For shared implementation with some abstract members
- **Concrete Class**: For full implementation that can be instantiated

---

## Type Assertions

Type assertions tell the TypeScript compiler to treat a value as a specific type:

### Basic Type Assertions
```typescript
// Angle bracket syntax (not recommended in JSX)
let someValue: any = "Hello World";
let strLength: number = (<string>someValue).length;

// As syntax (preferred)
let someValue2: any = "Hello World";
let strLength2: number = (someValue2 as string).length;
```

### Common Use Cases
```typescript
// DOM manipulation
const input = document.getElementById('user-input') as HTMLInputElement;
input.value = "Hello"; // Now TypeScript knows it has a 'value' property

// Working with JSON
const jsonString = '{"name": "John", "age": 30}';
const user = JSON.parse(jsonString) as { name: string; age: number };
console.log(user.name); // TypeScript knows about 'name' property

// API responses
interface ApiResponse {
  data: any;
  status: number;
}

async function fetchUser(id: number) {
  const response = await fetch(`/api/users/${id}`);
  const result = await response.json() as ApiResponse;
  return result.data as User;
}
```

### Non-null Assertion Operator
```typescript
// When you're sure a value is not null/undefined
function processUser(user: User | null) {
  // Without assertion - TypeScript error
  // console.log(user.name); // Error: Object is possibly null

  // With non-null assertion
  console.log(user!.name); // Tell TS that user is definitely not null

  // Better approach - type guard
  if (user) {
    console.log(user.name); // TypeScript knows user is not null here
  }
}

// DOM elements
const button = document.querySelector('.submit-btn')!; // Definitely exists
button.addEventListener('click', handleClick);
```

### Double Assertions (Escape Hatch)
```typescript
// When you need to assert to an unrelated type (use sparingly)
const value: unknown = "hello";
const num = value as unknown as number; // First to unknown, then to number

// Or using any
const num2 = value as any as number;
```

⚠️ **Warning**: Type assertions don't change the runtime behavior - they only affect compile-time type checking!

---

## Generics

Generics provide a way to create reusable components that work with multiple types while maintaining type safety.

### Basic Generics
```typescript
// Generic function
function identity<T>(arg: T): T {
  return arg;
}

// Usage
let stringResult = identity<string>("Hello");    // Type: string
let numberResult = identity<number>(42);         // Type: number
let boolResult = identity<boolean>(true);        // Type: boolean

// Type inference (TypeScript can infer the type)
let autoString = identity("Hello");              // TypeScript infers T as string
let autoNumber = identity(42);                   // TypeScript infers T as number

// Generic arrow function
const clone = <T>(obj: T): T => {
  return { ...obj };
};
```

### Generic Constraints
```typescript
// Constraint with extends
interface Lengthwise {
  length: number;
}

function logLength<T extends Lengthwise>(arg: T): T {
  console.log(arg.length); // Now we know arg has a length property
  return arg;
}

// Usage
logLength("Hello");           // OK - string has length
logLength([1, 2, 3]);         // OK - array has length
logLength({ length: 10 });    // OK - object has length
// logLength(42);             // Error - number doesn't have length

// Multiple constraints
interface Named {
  name: string;
}

interface Aged {
  age: number;
}

function processEntity<T extends Named & Aged>(entity: T): string {
  return `${entity.name} is ${entity.age} years old`;
}
```

### Generic Interfaces
```typescript
// Generic interface
interface Container<T> {
  value: T;
  getValue(): T;
  setValue(value: T): void;
}

// Implementation
class Box<T> implements Container<T> {
  constructor(public value: T) {}

  getValue(): T {
    return this.value;
  }

  setValue(value: T): void {
    this.value = value;
  }
}

// Usage
const stringBox = new Box<string>("Hello");
const numberBox = new Box<number>(42);

// Generic interface with multiple type parameters
interface Pair<T, U> {
  first: T;
  second: U;
}

const pair: Pair<string, number> = {
  first: "Hello",
  second: 42
};

// Generic interface extending
interface NamedContainer<T> extends Container<T> {
  name: string;
}

class NamedBox<T> implements NamedContainer<T> {
  constructor(public name: string, public value: T) {}

  getValue(): T {
    return this.value;
  }

  setValue(value: T): void {
    this.value = value;
  }
}
```

### Generic Classes
```typescript
// Basic generic class
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }

  peek(): T | undefined {
    return this.items[this.items.length - 1];
  }

  isEmpty(): boolean {
    return this.items.length === 0;
  }

  size(): number {
    return this.items.length;
  }
}

// Usage
const numberStack = new Stack<number>();
numberStack.push(1);
numberStack.push(2);
console.log(numberStack.pop()); // 2

const stringStack = new Stack<string>();
stringStack.push("Hello");
stringStack.push("World");
console.log(stringStack.peek()); // "World"

// Generic class with constraints
class Repository<T extends { id: string | number }> {
  private items: T[] = [];

  add(item: T): void {
    this.items.push(item);
  }

  findById(id: string | number): T | undefined {
    return this.items.find(item => item.id === id);
  }

  getAll(): T[] {
    return [...this.items];
  }

  remove(id: string | number): boolean {
    const index = this.items.findIndex(item => item.id === id);
    if (index !== -1) {
      this.items.splice(index, 1);
      return true;
    }
    return false;
  }
}

// Usage
interface User {
  id: number;
  name: string;
  email: string;
}

const userRepo = new Repository<User>();
userRepo.add({ id: 1, name: "John", email: "john@example.com" });
userRepo.add({ id: 2, name: "Jane", email: "jane@example.com" });

const user = userRepo.findById(1);
console.log(user?.name); // "John"
```

### Generic Multiple Types
```typescript
// Multiple generic parameters
function merge<T, U>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const merged = merge(
  { name: "John", age: 30 },
  { email: "john@example.com", isActive: true }
);
// merged has type: { name: string; age: number; email: string; isActive: boolean; }

// Generic function with multiple constraints
function compare<T extends string | number, U extends string | number>(
  a: T,
  b: U
): number {
  if (a < b) return -1;
  if (a > b) return 1;
  return 0;
}

// Three or more generic types
function transform<Input, Output, Error>(
  input: Input,
  transformer: (input: Input) => Output,
  errorHandler: (error: Error) => Output
): Output {
  try {
    return transformer(input);
  } catch (error) {
    return errorHandler(error as Error);
  }
}

// Generic tuple function
function swap<T, U>(tuple: [T, U]): [U, T] {
  return [tuple[1], tuple[0]];
}

const swapped = swap(["hello", 42]); // Type: [number, string]
```

### Advanced Generic Patterns

#### Conditional Types
```typescript
// Basic conditional type
type IsString<T> = T extends string ? true : false;

type Test1 = IsString<string>;  // true
type Test2 = IsString<number>;  // false

// Practical example
type ApiResponse<T> = T extends string 
  ? { message: T } 
  : { data: T };

type StringResponse = ApiResponse<string>;  // { message: string }
type NumberResponse = ApiResponse<number>;  // { data: number }

// Extract return type
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

function getString(): string { return "hello"; }
function getNumber(): number { return 42; }

type StringReturnType = ReturnType<typeof getString>;  // string
type NumberReturnType = ReturnType<typeof getNumber>;  // number
```

#### Mapped Types with Generics
```typescript
// Make all properties optional
type Partial<T> = {
  [P in keyof T]?: T[P];
};

// Make all properties required
type Required<T> = {
  [P in keyof T]-?: T[P];
};

// Make all properties readonly
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

// Pick specific properties
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

// Omit specific properties
type Omit<T, K extends keyof T> = Pick<T, Exclude<keyof T, K>>;

// Usage examples
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

type PartialUser = Partial<User>;        // All properties optional
type PublicUser = Omit<User, 'password'>; // User without password
type UserCredentials = Pick<User, 'email' | 'password'>; // Only email and password
```

#### Generic Utility Functions
```typescript
// Generic array utilities
class ArrayUtils {
  static first<T>(array: T[]): T | undefined {
    return array[0];
  }

  static last<T>(array: T[]): T | undefined {
    return array[array.length - 1];
  }

  static filter<T>(array: T[], predicate: (item: T) => boolean): T[] {
    return array.filter(predicate);
  }

  static map<T, U>(array: T[], mapper: (item: T) => U): U[] {
    return array.map(mapper);
  }

  static groupBy<T, K extends string | number | symbol>(
    array: T[],
    keySelector: (item: T) => K
  ): Record<K, T[]> {
    return array.reduce((groups, item) => {
      const key = keySelector(item);
      if (!groups[key]) {
        groups[key] = [];
      }
      groups[key].push(item);
      return groups;
    }, {} as Record<K, T[]>);
  }
}

// Usage
const users = [
  { name: "John", age: 25, department: "IT" },
  { name: "Jane", age: 30, department: "HR" },
  { name: "Bob", age: 35, department: "IT" }
];

const firstUser = ArrayUtils.first(users);
const usersByDept = ArrayUtils.groupBy(users, user => user.department);
const userNames = ArrayUtils.map(users, user => user.name);
```

### Generic Type Assertions
```typescript
// Generic type assertion function
function assertType<T>(value: unknown): asserts value is T {
  // Runtime validation would go here
  // For this example, we'll assume the assertion is always true
}

// Generic type guard
function isOfType<T>(value: unknown, validator: (val: unknown) => val is T): value is T {
  return validator(value);
}

// Usage
function isUser(value: unknown): value is User {
  return typeof value === 'object' && 
         value !== null && 
         'id' in value && 
         'name' in value && 
         'email' in value;
}

const unknownData: unknown = { id: 1, name: "John", email: "john@example.com" };

if (isOfType(unknownData, isUser)) {
  // TypeScript knows unknownData is User here
  console.log(unknownData.name);
}

// Generic factory pattern
interface Constructable<T = {}> {
  new (...args: any[]): T;
}

class Factory {
  static create<T>(ctor: Constructable<T>, ...args: any[]): T {
    return new ctor(...args);
  }
}

// Usage
class Person {
  constructor(public name: string, public age: number) {}
}

const person = Factory.create(Person, "John", 30);
```

---

## Best Practices and Tips

### Type Safety Best Practices
```typescript
// 1. Prefer explicit types for public APIs
export function processUser(user: User): UserResult {
  // Implementation
}

// 2. Use strict TypeScript configuration
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noImplicitReturns": true
  }
}

// 3. Use type guards instead of type assertions when possible
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

// Good
if (isString(someValue)) {
  console.log(someValue.toUpperCase());
}

// Less safe
console.log((someValue as string).toUpperCase());

// 4. Prefer interfaces over type aliases for object shapes
interface User {  // Preferred for objects
  name: string;
  email: string;
}

type Status = 'loading' | 'success' | 'error';  // Good for unions

// 5. Use readonly for immutable data
interface ReadonlyConfig {
  readonly apiUrl: string;
  readonly timeout: number;
}
```

### Common Patterns
```typescript
// Result pattern for error handling
type Result<T, E = Error> = 
  | { success: true; data: T }
  | { success: false; error: E };

async function fetchUser(id: number): Promise<Result<User>> {
  try {
    const user = await api.getUser(id);
    return { success: true, data: user };
  } catch (error) {
    return { success: false, error: error as Error };
  }
}

// Builder pattern with generics
class QueryBuilder<T> {
  private conditions: Array<(item: T) => boolean> = [];

  where(condition: (item: T) => boolean): this {
    this.conditions.push(condition);
    return this;
  }

  execute(data: T[]): T[] {
    return data.filter(item => 
      this.conditions.every(condition => condition(item))
    );
  }
}

// Usage
const results = new QueryBuilder<User>()
  .where(user => user.age > 18)
  .where(user => user.isActive)
  .execute(users);
```

---

## Summary

This comprehensive TypeScript guide covers:

✅ **Fundamentals**: Setup, basic types, and type annotations  
✅ **Functions**: Parameters, return types, and advanced function features  
✅ **Advanced Types**: Unions, intersections, literals, and type aliases  
✅ **Data Structures**: Arrays, tuples, and enums  
✅ **Object-Oriented**: Interfaces and classes with full feature coverage  
✅ **Type System**: Type assertions and type safety techniques  
✅ **Generics**: Complete coverage from basics to advanced patterns  

### Key Takeaways

1. **Type Safety**: TypeScript's main benefit is catching errors at compile time
2. **Gradual Adoption**: You can introduce TypeScript gradually into existing JavaScript projects
3. **Developer Experience**: Better IDE support, autocomplete, and refactoring tools
4. **Maintainability**: Types serve as living documentation for your code
5. **Team Collaboration**: Interfaces and types provide clear contracts between team members

### Next Steps

1. Practice with real projects
2. Explore advanced TypeScript features like decorators
3. Learn about TypeScript with popular frameworks (React, Node.js, etc.)
4. Study the TypeScript compiler options in depth
5. Contribute to TypeScript open-source projects

Remember: TypeScript is JavaScript with types - start simple and gradually adopt more advanced features as you become comfortable with the basics!