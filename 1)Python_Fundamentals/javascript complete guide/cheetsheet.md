# 📄 **JavaScript Quick Revision Cheat Sheet**

**Complete Reference | Hinglish Friendly | Interview Ready**

---

## **1. Variables & Data Types**

```javascript
// Variables (Hinglish: Variables declare karna)
let naam = "Rahul";      // Block-scoped, can reassign
const PI = 3.14;         // Block-scoped, cannot reassign
var old = "legacy";      // Function-scoped, avoid karo

// Data Types
let str = "string";      // String
let num = 42;            // Number
let bool = true;         // Boolean
let nothing = null;      // Null
let notDefined;          // Undefined
let sym = Symbol("id");  // Symbol
let big = 100n;          // BigInt
let obj = {};            // Object
```

---

## **2. Operators (Cheat Sheet)**

```javascript
// Arithmetic: +, -, *, /, %, **
5 + 3;    // 8
5 ** 2;   // 25 (power)

// Comparison (Hamesha === use karo)
5 === "5";   // false (strict)
5 == "5";    // true (loose, avoid karo)

// Logical: &&, ||, !
true && false;  // false
true || false;  // true
!true;          // false

// Nullish Coalescing & Optional Chaining
null ?? "default";    // "default"
obj?.prop?.nested;    // Safe access

// Spread & Rest
[...arr1, ...arr2];   // Spread
function(...args) {}  // Rest
```

---

## **3. Functions (Quick Reference)**

```javascript
// Function Declaration
function greet(naam) {
    return "Hello " + naam;
}

// Arrow Function (Modern, Hinglish: Arrow function use karo)
const add = (a, b) => a + b;
const square = x => x * x;  // Single param, no ()

// Default Parameters
function test(x = 10) { }

// Rest Parameters
function sum(...numbers) {
    return numbers.reduce((a, b) => a + b, 0);
}

// Higher-Order Function
const multiply = (factor) => (num) => num * factor;
const double = multiply(2);
double(5); // 10
```

---

## **4. Array Methods (Most Important)**

```javascript
const arr = [1, 2, 3, 4, 5];

// Transform (map)
arr.map(x => x * 2);           // [2, 4, 6, 8, 10]

// Filter
arr.filter(x => x > 2);        // [3, 4, 5]

// Reduce (most powerful)
arr.reduce((sum, x) => sum + x, 0);  // 15

// Find
arr.find(x => x > 3);          // 4 (first match)

// Some & Every
arr.some(x => x > 3);          // true (any)
arr.every(x => x > 0);         // true (all)

// Common operations
arr.push(6);     // End mein add
arr.pop();       // End se remove
arr.shift();     // Start se remove
arr.unshift(0);  // Start mein add
arr.slice(1, 3); // Extract [1, 2]
arr.splice(2, 1); // Remove at index 2
```

---

## **5. Object & Destructuring**

```javascript
// Object
const person = {
    naam: "Rahul",
    umar: 25,
    greet() {
        console.log(`Hello ${this.naam}`);
    }
};

// Destructuring (Hinglish: Values nikalna)
const { naam, umar } = person;
const [first, second, ...rest] = [1, 2, 3, 4, 5];

// Spread operator
const copy = { ...person, city: "Mumbai" };

// Object methods
Object.keys(person);    // ["naam", "umar", "greet"]
Object.values(person);  // ["Rahul", 25, function]
Object.entries(person); // [["naam", "Rahul"], ...]
```

---

## **6. this Keyword (4 Rules)**

```javascript
// 1. Default binding: global object
function test() {
    console.log(this); // Window/global
}

// 2. Implicit binding: object
const obj = {
    naam: "Rahul",
    greet() {
        console.log(this.naam); // "Rahul"
    }
};

// 3. Explicit binding: call/apply/bind
greet.call(obj, arg1, arg2);
greet.apply(obj, [arg1, arg2]);
const bound = greet.bind(obj);

// 4. new binding: constructor
function Person(naam) {
    this.naam = naam;
}
const p = new Person("Amit"); // new object

// Arrow functions: lexical this (outer scope ka use karte hain)
```

---

## **7. Promises & Async/Await**

```javascript
// Promise banao
const promise = new Promise((resolve, reject) => {
    if (success) resolve("Data");
    else reject("Error");
});

// Promise use karo
promise
    .then(data => console.log(data))
    .catch(error => console.log(error))
    .finally(() => console.log("Done"));

// Async/Await (Modern way)
async function fetchData() {
    try {
        const response = await fetch("url");
        const data = await response.json();
        return data;
    } catch (error) {
        console.error(error);
    }
}

// Parallel execution
const [d1, d2, d3] = await Promise.all([p1, p2, p3]);
```

---

## **8. Event Loop (Diagram)**

```
┌───────────────────────────┐
│   Call Stack              │  ← Sync code runs here
├───────────────────────────┤
│   Microtask Queue         │  ← Promises (.then)
│   (Higher Priority)       │
├───────────────────────────┤
│   Macrotask Queue         │  ← setTimeout, setInterval
│   (Lower Priority)        │
└───────────────────────────┘

Order: Sync → Microtasks → Macrotasks
```

```javascript
console.log("1");              // Sync
setTimeout(() => console.log("2"), 0); // Macrotask
Promise.resolve().then(() => console.log("3")); // Microtask
console.log("4");              // Sync

// Output: 1, 4, 3, 2
```

---

## **9. DOM Manipulation (Quick)**

```javascript
// Select elements
document.getElementById("id");
document.querySelector(".class");
document.querySelectorAll(".class");

// Create & modify
const div = document.createElement("div");
div.textContent = "Hello";
div.innerHTML = "<strong>Bold</strong>";
div.style.color = "red";
div.classList.add("active");
document.body.appendChild(div);

// Events
element.addEventListener("click", (e) => {
    console.log("Clicked", e.target);
});
```

---

## **10. ES6+ Features (Must Know)**

```javascript
// Template Literals
const naam = "Rahul";
console.log(`Hello ${naam}`);

// Destructuring
const { a, b } = obj;
const [x, y] = arr;

// Spread & Rest
const newArr = [...arr1, ...arr2];
function test(...args) {}

// Arrow Functions
const add = (a, b) => a + b;

// Default Parameters
function test(x = 10) {}

// Classes
class Person {
    constructor(naam) {
        this.naam = naam;
    }
    greet() {
        console.log(`Hello ${this.naam}`);
    }
}

// Optional Chaining & Nullish Coalescing
obj?.prop?.nested;
value ?? "default";

// Promises & Async/Await
async function fetchData() {
    const data = await fetch("url");
    return data.json();
}
```

---

## **11. Common Patterns (Interview Important)**

```javascript
// Debounce (Delay karo)
function debounce(func, delay) {
    let timer;
    return function(...args) {
        clearTimeout(timer);
        timer = setTimeout(() => func.apply(this, args), delay);
    };
}

// Throttle (Limit karo)
function throttle(func, limit) {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}

// Deep Clone
const clone = JSON.parse(JSON.stringify(obj));
// or
const clone = structuredClone(obj); // Modern

// Remove duplicates
const unique = [...new Set(arr)];

// Flatten array
const flat = arr.flat(Infinity);
```

---

## **12. Common Interview Traps (⚠️ Yaad rakho)**

```javascript
// 1. typeof null === "object" (Bug!)

// 2. == vs ===
0 == false;   // true (type coercion)
0 === false;  // false (strict)

// 3. Arrow function no 'this'
const obj = {
    naam: "Test",
    arrowFunc: () => {
        console.log(this.naam); // undefined!
    }
};

// 4. Var in loops
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 0);
}
// Prints: 3, 3, 3 (use 'let' instead)

// 5. Floating point
0.1 + 0.2 === 0.3; // false!

// 6. Object reference
let a = [1, 2];
let b = a;  // Same reference!
b.push(3);
console.log(a); // [1, 2, 3]
```

---

## **13. Quick Tips (Hinglish Mein)**

✅ **Always use `===` instead of `==`** (Type coercion avoid karo)
✅ **Use `const` by default, `let` jahan zaroorat ho** (var bhool jao)
✅ **Arrow functions for callbacks** (short aur clean)
✅ **Async/await over .then()** (readable code)
✅ **Use template literals** (string concatenation se better)
✅ **Optional chaining for safe access** (?. use karo)
✅ **Destructuring for cleaner code** (values easily nikalo)
✅ **Spread operator for copying** (arrays aur objects)

---

## **14. Performance Tips**

```javascript
// ❌ Avoid
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}

// ✅ Better
const len = arr.length;
for (let i = 0; i < len; i++) {
    console.log(arr[i]);
}

// ✅ Best (for simple iterations)
arr.forEach(item => console.log(item));

// Debounce expensive operations
const debouncedSearch = debounce(searchFunction, 300);
```

---

## **15. Must Remember for Interviews**

### **Scope Chain**
Inner → Outer → Global

### **Prototype Chain**
Instance → Constructor.prototype → Object.prototype → null

### **Event Loop Order**
1. Synchronous code
2. Microtasks (Promises)
3. Macrotasks (setTimeout)

### **Hoisting**
- `var`: Hoisted, initialized with undefined
- `let`/`const`: Hoisted, not initialized (TDZ)
- Functions: Fully hoisted

### **Closures**
Inner function + outer variables = Closure

---

## **16. One-Liners (Interview Mein Impress Karo)**

```javascript
// Check if array
Array.isArray(arr);

// Sum array
arr.reduce((a, b) => a + b, 0);

// Max value
Math.max(...arr);

// Remove duplicates
[...new Set(arr)];

// Shuffle array
arr.sort(() => Math.random() - 0.5);

// Deep clone
structuredClone(obj);

// Check empty object
Object.keys(obj).length === 0;

// Reverse string
str.split("").reverse().join("");

// Capitalize first letter
str.charAt(0).toUpperCase() + str.slice(1);

// Random number (0-n)
Math.floor(Math.random() * (n + 1));
```

---

**🎯 Key Takeaway (Hinglish):**
Yeh cheat sheet ko bookmark kar lo! Interview se pehle ek baar zaroor revise karo. Practice karte raho aur confident raho! 💪

**All the best! Happy Coding! 🚀**

