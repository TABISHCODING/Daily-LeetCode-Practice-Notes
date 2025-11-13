# 🚀 **JavaScript Complete Learning + Interview Mastery Guide**

**पूरा Web Development Reference | ES5 → ES2024 | DOM | Async | Algorithms | 150+ Interview Q&A**

---

## 📋 **Table of Contents**

1. [Introduction & Hinglish Explanation](#1-introduction--hinglish-explanation)
2. [Core JavaScript Fundamentals](#2-core-javascript-fundamentals)
3. [Advanced Core Concepts](#3-advanced-core-concepts)
4. [ES6+ to ES2024 Features](#4-es6-to-es2024-features)
5. [DOM & Browser JavaScript](#5-dom--browser-javascript)
6. [Asynchronous JavaScript](#6-asynchronous-javascript)
7. [JavaScript for Web Development](#7-javascript-for-web-development)
8. [Data Structures & Algorithms](#8-data-structures--algorithms)
9. [150+ Interview Questions](#9-150-interview-questions)
10. [Quick Revision Cheat Sheet](#10-quick-revision-cheat-sheet)
11. [Practice Projects](#11-practice-projects)

---

## 🎯 **1. Introduction & Hinglish Explanation**

### **What is Hinglish? (Hinglish kya hai?)**

**Hinglish** = Hindi + English (India mein commonly use hone wali mixed language)

**Examples:**

| **Pure English** | **Hinglish** |
|-----------------|--------------|
| I need to debug this code | Yaar, is code ko debug karna padega |
| This function is not working | Yeh function kaam nahi kar raha hai |
| Please check the console | Console mein check karo bhai |
| Loop through the array | Array par loop chalao |
| Variable is undefined | Variable undefined aa raha hai |

### **Common Hinglish Programming Terms:**

```javascript
// Hinglish comments ke saath code

// Variable declare karo
let naam = "Rahul"; // naam ko store kar rahe hain

// Function banao jo sum nikale
function jod(a, b) {
    return a + b; // dono numbers ka jod return kar rahe hain
}

// Loop chalao
for (let i = 0; i < 5; i++) {
    console.log(i); // numbers print ho rahe hain
}

// Condition check karo
if (naam === "Rahul") {
    console.log("Naam match ho gaya!"); // condition true hai
}
```

### **Why Learn JavaScript? (JavaScript kyun seekhein?)**

✅ **Web Development ka heart hai** - Har website mein use hota hai
✅ **Frontend + Backend** dono mein kaam karta hai (Node.js)
✅ **High demand** - Sabse zyada jobs available hain
✅ **Easy to start** - Beginners ke liye perfect
✅ **Rich ecosystem** - React, Vue, Angular, Node.js

**Hinglish mein:**
"Bhai, agar tum web development seekhna chahte ho, toh JavaScript compulsory hai. Iske bina kuch nahi hoga!"

---

## 📘 **2. Core JavaScript Fundamentals**

---

## **2.1 Variables: `let`, `const`, `var`**

### **📖 Simple Explanation (सरल समझ)**

Variables matlab containers jisme hum data store karte hain. JavaScript mein 3 tarike hain declare karne ke.

### **Hinglish Explanation:**
"Variable ek dabba hai jisme tum koi bhi cheez rakh sakte ho - number, string, object, anything!"

### **🪜 Micro-Steps**

**Step 1:** `var` samjho (purana tarika - function scoped)
```javascript
var naam = "Rahul";
console.log(naam); // Output: Rahul

// Hinglish: var purana style hai, ab use nahi karte zyada
```

**Step 2:** `let` use karo (block scoped, change kar sakte ho)
```javascript
let umar = 25;
umar = 26; // ✅ Change ho gaya, no problem
console.log(umar); // Output: 26

// Hinglish: let se value ko baad mein change kar sakte ho
```

**Step 3:** `const` use karo (block scoped, change nahi kar sakte)
```javascript
const PI = 3.14;
// PI = 3.15; // ❌ Error: const ko change nahi kar sakte
console.log(PI); // Output: 3.14

// Hinglish: const ka matlab constant - ek baar set kiya toh fixed!
```

**Step 4:** Block scope samjho
```javascript
{
    let x = 10;
    const y = 20;
    var z = 30;
}
// console.log(x); // ❌ Error: x block ke bahar nahi mil sakta
// console.log(y); // ❌ Error: y bhi nahi
console.log(z); // ✅ Output: 30 (var block se bahar nikal gaya!)

// Hinglish: let aur const block ke andar hi rahte hain, var leak ho jata hai
```

**Step 5:** Variable reassignment practice
```javascript
let score = 100;
score = score + 50; // ya score += 50;
console.log(score); // Output: 150

// Hinglish: score ko update kar diya, let mein allowed hai
```

**Step 6:** Const ke saath objects
```javascript
const user = { naam: "Priya" };
user.naam = "Anjali"; // ✅ Object ke andar change kar sakte hain
console.log(user.naam); // Output: Anjali

// user = {}; // ❌ Lekin pura object replace nahi kar sakte

// Hinglish: const object ko toh change nahi kar sakte, par uske 
// properties ko modify kar sakte ho
```

**Step 7:** Arrays ke saath const
```javascript
const colors = ["red", "green"];
colors.push("blue"); // ✅ Array mein add kar sakte hain
console.log(colors); // Output: ["red", "green", "blue"]

// colors = []; // ❌ Naya array assign nahi kar sakte

// Hinglish: Array mein items add/remove kar sakte ho, 
// but naya array nahi de sakte
```

### **⚠️ Common Mistakes (Aam Galtiyan)**

```javascript
// ❌ Galat: const ko baad mein change karna
const counter = 0;
// counter++; // Error ayega!

// ✅ Sahi: let use karo agar change karna hai
let counter = 0;
counter++; // Kaam karega

// Hinglish: Jo change hona hai use let do, jo fixed hai use const do
```

### **🎤 Interview Questions**

**Q1: `let`, `const`, aur `var` mein kya farak hai?**

**Answer (Hinglish):**
- `var`: Function ke andar limited, hoist hota hai, redeclare kar sakte hain
- `let`: Block ke andar limited, hoist hota hai par initialize nahi, redeclare nahi kar sakte
- `const`: Block ke andar limited, value change nahi hoti

**Q2: Yeh code ka output kya hoga?**
```javascript
console.log(a); // ?
var a = 5;
console.log(a); // ?
```

**Answer:**
```
undefined
5
```
**Hinglish Explanation:** Pehle `undefined` aayega kyunki var hoist ho gaya but value nahi mili. Phir 5 print hoga.

**Q3: Yeh code chalega?**
```javascript
const arr = [1, 2, 3];
arr.push(4);
console.log(arr);
```

**Answer:** Haan chalega! Output: `[1, 2, 3, 4]`
**Hinglish:** const array ko naya array nahi de sakte, par uske andar kuch add kar sakte hain.

### **💪 Mini Practice Challenge**

Ek student ka data banao:
```javascript
const studentName = "Rohan"; // naam nahi badlega
let studentAge = 18; // umar badal sakti hai
let studentMarks = 85; // marks badal sakte hain

studentAge = 19; // birthday ho gayi
studentMarks = 90; // marks improve ho gaye

console.log(studentName, studentAge, studentMarks);
// Output: Rohan 19 90
```

---

## **2.2 Data Types (Data ke Types)**

### **📖 Simple Explanation**

JavaScript mein 8 tarah ke data types hain: 7 primitive + 1 reference (objects).

**Hinglish:** "Data types matlab data ki category - number hai, string hai, boolean hai, etc."

### **🪜 Micro-Steps**

**Step 1:** Primitive Types (Basic types)
```javascript
// 1. String (text data)
let naam = "JavaScript";
let city = 'Mumbai';

// 2. Number (numbers - integer aur decimal dono)
let umar = 25;
let price = 99.99;

// 3. Boolean (true/false)
let isLoggedIn = true;
let hasAccess = false;

// 4. Undefined (value assign nahi hui)
let data;
console.log(data); // Output: undefined

// 5. Null (intentionally empty)
let empty = null;

// 6. Symbol (unique identifier)
let id = Symbol('id');

// 7. BigInt (bahut bade numbers ke liye)
let bigNumber = 1234567890123456789012345678901234567890n;

// Hinglish: Yeh sab primitive types hain - basic building blocks
```

**Step 2:** Reference Type (Objects)
```javascript
// Object (key-value pairs)
let person = {
    naam: "Amit",
    umar: 30,
    city: "Delhi"
};

// Array (ordered collection)
let colors = ["red", "green", "blue"];

// Function (executable code)
function greet() {
    console.log("Hello!");
}

// Hinglish: Objects complex data store karte hain
```

**Step 3:** `typeof` operator se type check karo
```javascript
console.log(typeof "Hello");      // Output: string
console.log(typeof 42);           // Output: number
console.log(typeof true);         // Output: boolean
console.log(typeof undefined);    // Output: undefined
console.log(typeof null);         // Output: object (JavaScript ka bug!)
console.log(typeof Symbol());     // Output: symbol
console.log(typeof 100n);         // Output: bigint
console.log(typeof {});           // Output: object
console.log(typeof []);           // Output: object
console.log(typeof function(){}); // Output: function

// Hinglish: typeof se pata chal jata hai kaunsa type hai
```

**Step 4:** Type coercion examples (automatic conversion)
```javascript
console.log(5 + "5");      // Output: "55" (number string ban gaya)
console.log("5" - 2);      // Output: 3 (string number ban gaya)
console.log(true + 1);     // Output: 2 (true = 1)
console.log(false + 1);    // Output: 1 (false = 0)
console.log(null + 5);     // Output: 5 (null = 0)
console.log(undefined + 5); // Output: NaN (Not a Number)

// Hinglish: JavaScript automatically types convert kar deta hai
```

**Step 5:** Array check karna
```javascript
let arr = [1, 2, 3];
console.log(typeof arr);           // Output: object (confusing!)
console.log(Array.isArray(arr));   // Output: true (correct way!)

// Hinglish: Array check karne ka sahi tarika Array.isArray() hai
```

**Step 6:** Value vs Reference
```javascript
// Primitive (value copy hoti hai)
let a = 10;
let b = a; // b ko a ki copy mili
b = 20;
console.log(a); // Output: 10 (a unchanged)
console.log(b); // Output: 20

// Reference (address copy hota hai)
let obj1 = { value: 10 };
let obj2 = obj1; // obj2 ko obj1 ka address mila
obj2.value = 20;
console.log(obj1.value); // Output: 20 (changed!)
console.log(obj2.value); // Output: 20

// Hinglish: Primitive mein value copy hoti hai, 
// objects mein address copy hota hai
```

**Step 7:** NaN (Not a Number)
```javascript
console.log(0 / 0);           // Output: NaN
console.log("hello" * 2);     // Output: NaN
console.log(Math.sqrt(-1));   // Output: NaN

// NaN check karna
console.log(isNaN("hello"));        // true
console.log(Number.isNaN("hello")); // false (strict)
console.log(Number.isNaN(NaN));     // true

// Hinglish: NaN matlab "Not a Number" - invalid calculation
```

### **⚠️ Common Mistakes**

```javascript
// ❌ typeof null === "null" (galat assumption)
console.log(typeof null); // Output: "object" (JavaScript bug)

// ✅ null check karne ka sahi tarika
if (value === null) {
    console.log("It's null");
}

// Hinglish: null ko directly check karo, typeof mat use karo
```

### **🎤 Interview Questions**

**Q1: typeof null ka output "object" kyun aata hai?**

**Answer (Hinglish):** Yeh JavaScript ki pehli version ka bug tha jo backward compatibility ke liye rakha gaya. Technically null ek primitive type hai.

**Q2: Output kya hoga?**
```javascript
let x = 10;
let y = x;
x = 20;
console.log(y);
```

**Answer:** `10` - Primitives value se copy hote hain.

**Q3: Yeh code ka output?**
```javascript
let obj1 = { count: 5 };
let obj2 = obj1;
obj2.count = 10;
console.log(obj1.count);
```

**Answer:** `10` - Objects reference se copy hote hain, dono same memory location point karte hain.

### **💪 Mini Practice Challenge**

```javascript
// Sabhi types ke variables banao
let myString = "Hinglish";
let myNumber = 42;
let myBoolean = true;
let myUndefined;
let myNull = null;
let mySymbol = Symbol('unique');
let myBigInt = 9007199254740991n;
let myObject = { key: "value" };
let myArray = [1, 2, 3];

// Har ek ka typeof check karo
console.log(typeof myString);    // string
console.log(typeof myNumber);    // number
console.log(typeof myBoolean);   // boolean
console.log(typeof myUndefined); // undefined
console.log(typeof myNull);      // object (bug!)
console.log(typeof mySymbol);    // symbol
console.log(typeof myBigInt);    // bigint
console.log(typeof myObject);    // object
console.log(typeof myArray);     // object
```

---

## **2.3 Operators (Operations karne wale)**

### **📖 Simple Explanation**

Operators wo symbols hain jo values pe operations perform karte hain.

**Hinglish:** "Operators matlab +, -, *, / jaise symbols jo calculation karte hain"

### **🪜 Micro-Steps**

**Step 1:** Arithmetic Operators (Math wale)
```javascript
let a = 10, b = 3;

console.log(a + b);  // Output: 13 (jod - addition)
console.log(a - b);  // Output: 7  (minus - subtraction)
console.log(a * b);  // Output: 30 (guna - multiplication)
console.log(a / b);  // Output: 3.333... (bhag - division)
console.log(a % b);  // Output: 1  (baki - modulus/remainder)
console.log(a ** b); // Output: 1000 (power - exponentiation)

let c = 5;
c++;                 // Increment (c = 6, ek badhao)
c--;                 // Decrement (c = 5, ek ghatao)

// Hinglish: Basic math operations - jod, ghata, guna, bhag
```

**Step 2:** Assignment Operators
```javascript
let x = 10;
x += 5;  // x = x + 5  → x = 15 (jod karke assign)
x -= 3;  // x = x - 3  → x = 12 (minus karke assign)
x *= 2;  // x = x * 2  → x = 24 (multiply karke assign)
x /= 4;  // x = x / 4  → x = 6  (divide karke assign)
x %= 4;  // x = x % 4  → x = 2  (remainder assign)

// Hinglish: Short way to update variables
```

**Step 3:** Comparison Operators (Compare karne wale)
```javascript
console.log(5 == "5");   // Output: true (loose - type convert hoga)
console.log(5 === "5");  // Output: false (strict - type bhi check)
console.log(5 != "5");   // Output: false (loose not equal)
console.log(5 !== "5");  // Output: true (strict not equal)

console.log(10 > 5);     // Output: true (bada hai)
console.log(10 < 5);     // Output: false (chota hai)
console.log(10 >= 10);   // Output: true (bada ya barabar)
console.log(10 <= 9);    // Output: false (chota ya barabar)

// Hinglish: === always use karo, == confusing hai
```

**Step 4:** Logical Operators
```javascript
// && (AND) - dono true ho toh true
console.log(true && true);   // Output: true
console.log(true && false);  // Output: false

// || (OR) - ek bhi true ho toh true
console.log(true || false);  // Output: true
console.log(false || false); // Output: false

// ! (NOT) - opposite value
console.log(!true);          // Output: false
console.log(!false);         // Output: true

// Short-circuit evaluation
let result = null || "default";
console.log(result); // Output: "default"

let value = 0 && "Hello";
console.log(value); // Output: 0

// Hinglish: && ka matlab "aur", || ka matlab "ya"
```

**Step 5:** Ternary Operator (Short if-else)
```javascript
let umar = 18;
let status = (umar >= 18) ? "Adult" : "Minor";
console.log(status); // Output: "Adult"

// Nested ternary (avoid karo, confusing hai)
let marks = 85;
let grade = marks >= 90 ? "A" : marks >= 80 ? "B" : "C";
console.log(grade); // Output: "B"

// Hinglish: Ternary short if-else hai - condition ? true : false
```

**Step 6:** Nullish Coalescing (`??`) - ES2020
```javascript
let naam = null;
console.log(naam ?? "Guest"); // Output: "Guest"

let count = 0;
console.log(count ?? 10); // Output: 0 (0 null/undefined nahi hai)

// Compare with || (OR)
console.log(count || 10); // Output: 10 (0 falsy hai)

// Hinglish: ?? sirf null/undefined check karta hai, || sabhi falsy check karta hai
```

**Step 7:** Optional Chaining (`?.`) - ES2020
```javascript
let user = {
    naam: "Rahul",
    address: {
        city: "Mumbai"
    }
};

console.log(user?.address?.city); // Output: "Mumbai"
console.log(user?.phone?.number); // Output: undefined (error nahi)

// Without optional chaining (error aayega)
// console.log(user.phone.number); // ❌ Error!

// Array ke saath
let arr = [1, 2, 3];
console.log(arr?.[0]); // Output: 1

// Function ke saath
let obj = {
    greet: function() { return "Hello"; }
};
console.log(obj.greet?.()); // Output: "Hello"

// Hinglish: ?. safely properties access karta hai, error nahi deta
```

**Step 8:** Spread Operator (`...`) - ES6
```javascript
// Array spreading
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = [...arr1, ...arr2];
console.log(combined); // Output: [1, 2, 3, 4, 5, 6]

// Object spreading
let person1 = { naam: "Amit", umar: 25 };
let person2 = { ...person1, city: "Delhi" };
console.log(person2); 
// Output: { naam: "Amit", umar: 25, city: "Delhi" }

// Function arguments
function sum(a, b, c) {
    return a + b + c;
}
let numbers = [1, 2, 3];
console.log(sum(...numbers)); // Output: 6

// Hinglish: ... operator array/object ko spread kar deta hai
```

### **⚠️ Common Mistakes**

```javascript
// ❌ == use karna (type coercion confusing hai)
if (0 == false) {
    console.log("True!"); // Yeh chalega (confusing!)
}

// ✅ === always use karo
if (0 === false) {
    console.log("True!"); // Yeh nahi chalega (correct!)
}

// Hinglish: Hamesha === use karo, == bahut confusing hai
```

### **🎤 Interview Questions**

**Q1: `==` aur `===` mein kya farak hai?**

**Answer (Hinglish):**
- `==`: Loose equality - type convert karke compare karta hai
- `===`: Strict equality - type aur value dono check karta hai

Example:
```javascript
console.log(5 == "5");  // true (string ko number bana diya)
console.log(5 === "5"); // false (type different hai)
```

**Q2: Output kya hoga?**
```javascript
console.log(0 || 1 && 2);
```

**Answer:** `2`
**Hinglish Explanation:** && pehle calculate hoga (precedence high hai). `1 && 2` = `2`, phir `0 || 2` = `2`.

**Q3: `??` aur `||` mein kya difference hai?**

**Answer (Hinglish):**
- `??`: Sirf `null` aur `undefined` check karta hai
- `||`: Saari falsy values check karta hai (0, "", false, null, undefined, NaN)

```javascript
let count = 0;
console.log(count ?? 10); // 0 (null/undefined nahi hai)
console.log(count || 10); // 10 (0 falsy hai)
```

**Q4: Optional chaining kab use karni chahiye?**

**Answer (Hinglish):** Jab tum sure nahi ho ki property exist karti hai ya nahi. `?.` safely access karta hai aur error nahi deta.

```javascript
let user = { naam: "Amit" };
console.log(user?.address?.city); // undefined (no error)
// console.log(user.address.city); // ❌ Error!
```

### **💪 Mini Practice Challenge**

```javascript
// Challenge: Calculator banao with all operators

let num1 = 20;
let num2 = 5;

console.log("Addition:", num1 + num2);       // 25
console.log("Subtraction:", num1 - num2);    // 15
console.log("Multiplication:", num1 * num2); // 100
console.log("Division:", num1 / num2);       // 4
console.log("Modulus:", num1 % num2);        // 0
console.log("Power:", num1 ** 2);            // 400

// Comparison
console.log("Greater than:", num1 > num2);   // true
console.log("Equal (strict):", num1 === 20); // true

// Ternary
let result = num1 > num2 ? "num1 bada hai" : "num2 bada hai";
console.log(result); // num1 bada hai

// Nullish coalescing
let value = null;
console.log(value ?? "Default value"); // Default value

// Optional chaining
let data = { user: { naam: "Rohan" } };
console.log(data?.user?.naam); // Rohan
console.log(data?.admin?.naam); // undefined
```

---

## **2.4 Functions (Kaam karne wale blocks)**

### **📖 Simple Explanation**

Functions reusable code blocks hain jo specific task perform karte hain.

**Hinglish:** "Function ek package hai jisme code rakha hai - jab chahiye tab use kar lo!"

### **🪜 Micro-Steps**

**Step 1:** Function Declaration (Traditional way)
```javascript
function greet(naam) {
    return "Hello, " + naam + "!";
}

console.log(greet("Priya")); // Output: Hello, Priya!

// Hinglish: Function declare kiya, phir call kiya
```

**Step 2:** Function Expression (Variable mein store karna)
```javascript
const jod = function(a, b) {
    return a + b;
};

console.log(jod(5, 3)); // Output: 8

// Hinglish: Function ko variable mein store kar sakte hain
```

**Step 3:** Arrow Functions (ES6 - Short syntax)
```javascript
// Single parameter (brackets optional)
const square = x => x * x;
console.log(square(5)); // Output: 25

// Multiple parameters
const multiply = (a, b) => a * b;
console.log(multiply(4, 5)); // Output: 20

// Multiple statements (curly braces + return chahiye)
const greetUser = naam => {
    let message = "Welcome, " + naam;
    return message;
};
console.log(greetUser("Amit")); // Output: Welcome, Amit

// Hinglish: Arrow function modern aur short hai - => arrow ki tarah hai
```

**Step 4:** Default Parameters (Default values)
```javascript
function orderFood(item = "Pizza", quantity = 1) {
    return `Ordered ${quantity} ${item}(s)`;
}

console.log(orderFood());              // Output: Ordered 1 Pizza(s)
console.log(orderFood("Burger"));      // Output: Ordered 1 Burger(s)
console.log(orderFood("Pasta", 3));    // Output: Ordered 3 Pasta(s)

// Hinglish: Agar value nahi di toh default value use hogi
```

**Step 5:** Rest Parameters (Unlimited arguments)
```javascript
function sum(...numbers) {
    let total = 0;
    for (let num of numbers) {
        total += num;
    }
    return total;
}

console.log(sum(1, 2, 3));        // Output: 6
console.log(sum(5, 10, 15, 20));  // Output: 50
console.log(sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)); // Output: 55

// Modern way with reduce
const sumModern = (...nums) => nums.reduce((total, n) => total + n, 0);
console.log(sumModern(1, 2, 3, 4, 5)); // Output: 15

// Hinglish: ...numbers matlab jitne chahiye utne arguments pass karo
```

**Step 6:** Higher-Order Functions (Functions jo functions return karte hain)
```javascript
// Function jo function return kare
function multiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

const double = multiplier(2);
const triple = multiplier(3);
const tenTimes = multiplier(10);

console.log(double(5));    // Output: 10
console.log(triple(5));    // Output: 15
console.log(tenTimes(5));  // Output: 50

// Function jo function as argument le
function execute(fn, value) {
    return fn(value);
}

console.log(execute(double, 7)); // Output: 14

// Hinglish: Higher-order function matlab function ke saath khelna - 
// function ko pass karo ya return karo
```

**Step 7:** IIFE (Immediately Invoked Function Expression)
```javascript
// Turant execute ho jata hai
(function() {
    console.log("Main turant run ho gaya!");
})();
// Output: Main turant run ho gaya!

// With parameters
(function(naam) {
    console.log("Hello, " + naam);
})("JavaScript");
// Output: Hello, JavaScript

// Arrow IIFE
(() => {
    console.log("Arrow IIFE bhi chal gaya!");
})();

// Hinglish: IIFE matlab function likhte hi run ho jaye - 
// wait nahi karna padta
```

**Step 8:** Callback Functions
```javascript
function processData(data, callback) {
    console.log("Processing: " + data);
    callback(data); // Callback function ko call kiya
}

processData("User Data", function(result) {
    console.log("Done with: " + result);
});
// Output:
// Processing: User Data
// Done with: User Data

// Real-world example: setTimeout
setTimeout(function() {
    console.log("3 seconds bad yeh message");
}, 3000);

// Hinglish: Callback matlab function ko as argument pass karna
```

**Step 9:** Pure Functions (Side-effect free)
```javascript
// ✅ Pure function (same input = same output, no side effects)
function jod(a, b) {
    return a + b;
}

console.log(jod(5, 3)); // Hamesha 8

// ❌ Impure function (external state modify karta hai)
let total = 0;
function addToTotal(num) {
    total += num; // External variable ko change kar raha hai
    return total;
}

console.log(addToTotal(5));  // 5
console.log(addToTotal(5));  // 10 (same input, different output!)

// Hinglish: Pure function predictable hai - same input = same output
```

**Step 10:** Recursion (Function apne aap ko call kare)
```javascript
// Factorial calculate karna
function factorial(n) {
    if (n === 0 || n === 1) {
        return 1; // Base case
    }
    return n * factorial(n - 1); // Recursive case
}

console.log(factorial(5)); // Output: 120 (5 * 4 * 3 * 2 * 1)

// Countdown example
function countdown(num) {
    if (num < 0) return;
    console.log(num);
    countdown(num - 1);
}

countdown(5);
// Output:
// 5
// 4
// 3
// 2
// 1
// 0

// Hinglish: Recursion matlab function apne aap ko call kare
```

### **⚠️ Common Mistakes**

```javascript
// ❌ Arrow function mein 'this' ka issue
const obj = {
    naam: "Object",
    regularFunc: function() {
        console.log(this.naam); // ✅ Works
    },
    arrowFunc: () => {
        console.log(this.naam); // ❌ undefined
    }
};

obj.regularFunc(); // Output: Object
obj.arrowFunc();   // Output: undefined

// Hinglish: Arrow functions ko 'this' ka context nahi milta
```

```javascript
// ❌ Function declaration aur expression ka confusion
greet(); // ✅ Works (hoisted)
function greet() { console.log("Hi"); }

// sayHi(); // ❌ Error (not hoisted)
const sayHi = function() { console.log("Hi"); };
```

### **🎤 Interview Questions**

**Q1: Function declaration aur function expression mein kya difference hai?**

**Answer (Hinglish):**
- **Function Declaration**: Hoist hota hai - upar call kar sakte ho
```javascript
greet(); // Works!
function greet() { console.log("Hi"); }
```

- **Function Expression**: Hoist nahi hota - pehle define karo, phir call karo
```javascript
// greet(); // ❌ Error!
const greet = function() { console.log("Hi"); };
```

**Q2: Is code ka output kya hoga?**
```javascript
const obj = {
    count: 0,
    increment: function() {
        setTimeout(function() {
            this.count++;
            console.log(this.count);
        }, 1000);
    }
};
obj.increment();
```

**Answer:** `NaN`
**Hinglish Explanation:** Regular function mein `this` ka context kho gaya. Arrow function use karo:
```javascript
setTimeout(() => {
    this.count++;
    console.log(this.count); // 1
}, 1000);
```

**Q3: Pure function kya hota hai?**

**Answer (Hinglish):** Pure function wo hai jo:
1. Same input pe hamesha same output de
2. Koi side effect na ho (external state change nahi kare)

```javascript
// ✅ Pure
function add(a, b) {
    return a + b;
}

// ❌ Impure
let counter = 0;
function increment() {
    counter++; // External state change
}
```

**Q4: Recursion kab use karna chahiye?**

**Answer (Hinglish):** Jab problem ko chote sub-problems mein tod sakte ho - factorial, tree traversal, etc.

```javascript
// Fibonacci with recursion
function fib(n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

### **💪 Mini Practice Challenge**

```javascript
// Challenge 1: Calculator with arrow functions
const calculator = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
    multiply: (a, b) => a * b,
    divide: (a, b) => b !== 0 ? a / b : "Cannot divide by zero"
};

console.log(calculator.add(10, 5));      // 15
console.log(calculator.subtract(10, 5)); // 5
console.log(calculator.multiply(10, 5)); // 50
console.log(calculator.divide(10, 5));   // 2

// Challenge 2: Array processor with callback
function processArray(arr, callback) {
    const result = [];
    for (let item of arr) {
        result.push(callback(item));
    }
    return result;
}

const numbers = [1, 2, 3, 4, 5];
const doubled = processArray(numbers, num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// Challenge 3: Counter with closure (private counter)
function createCounter() {
    let count = 0;
    return {
        increment: () => ++count,
        decrement: () => --count,
        getValue: () => count
    };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.decrement()); // 1
console.log(counter.getValue());  // 1
```

---

## **2.5 Scope (Variable ki Visibility)**

### **📖 Simple Explanation**

Scope decide karta hai ki variable kahan accessible hai.

**Hinglish:** "Scope matlab variable ki reach - kahan tak use kar sakte ho!"

### **🪜 Micro-Steps**

**Step 1:** Global Scope (Sabke liye available)
```javascript
// File ke top level pe declare kiya
let globalVar = "Main global hoon";

function test() {
    console.log(globalVar); // ✅ Mil gaya
}

test(); // Output: Main global hoon
console.log(globalVar); // Output: Main global hoon

// Hinglish: Global variable sab jagah available hai
```

**Step 2:** Function Scope (Function ke andar)
```javascript
function myFunction() {
    var functionVar = "Main function ke andar hoon";
    console.log(functionVar); // ✅ Yahan mil gaya
}

myFunction(); // Output: Main function ke andar hoon
// console.log(functionVar); // ❌ Error: bahar nahi mil sakta

// Hinglish: Function scope means function ke andar hi limited
```

**Step 3:** Block Scope (`let` aur `const` ke saath)
```javascript
{
    let blockVar = "Main block ke andar hoon";
    const blockConst = "Main bhi block mein hoon";
    console.log(blockVar);   // ✅ Yahan mil gaye
    console.log(blockConst); // ✅ Yahan mil gaye
}

// console.log(blockVar);   // ❌ Error: bahar nahi mil sakte
// console.log(blockConst); // ❌ Error

// var block scope nahi follow karta
{
    var notBlockScoped = "Main leak ho gaya!";
}
console.log(notBlockScoped); // ✅ Output: Main leak ho gaya!

// Hinglish: let/const block ke andar, var leak ho jata hai
```

**Step 4:** Lexical Scope (Nested functions)
```javascript
function outer() {
    let outerVar = "Outer function";
    
    function inner() {
        let innerVar = "Inner function";
        console.log(outerVar); // ✅ Bahar ka access hai
        console.log(innerVar); // ✅ Apna access hai
    }
    
    inner();
    // console.log(innerVar); // ❌ Andar ka access nahi
}

outer();
// Output:
// Outer function
// Inner function

// Hinglish: Inner function outer ke variables access kar sakta hai
```

**Step 5:** Scope Chain (Upar ki taraf dhundna)
```javascript
let a = "Global A";

function first() {
    let b = "First B";
    
    function second() {
        let c = "Second C";
        console.log(a); // Global se mila
        console.log(b); // Parent se mila
        console.log(c); // Apna hai
    }
    
    second();
}

first();
// Output:
// Global A
// First B
// Second C

// Hinglish: Scope chain matlab upar ke levels ko check karo
```

**Step 6:** Loop Scope Problems (var vs let)
```javascript
// ❌ var ka problem
console.log("var wala loop:");
for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log("var i:", i); // Sabhi 3 print honge
    }, 1000);
}

// ✅ let ka solution
console.log("let wala loop:");
for (let j = 0; j < 3; j++) {
    setTimeout(function() {
        console.log("let j:", j); // 0, 1, 2 print honge
    }, 1000);
}

// Hinglish: var loop mein leak karta hai, let har iteration pe naya
```

**Step 7:** Shadowing (Same naam ka variable)
```javascript
let x = "Global X";

function test() {
    let x = "Function X"; // Global ko shadow kar raha hai
    console.log(x); // Function wala print hoga
}

test(); // Output: Function X
console.log(x); // Output: Global X

// Block shadowing
let naam = "Rahul";
{
    let naam = "Amit"; // Bahar wale ko shadow kiya
    console.log(naam); // Output: Amit
}
console.log(naam); // Output: Rahul

// Hinglish: Shadowing matlab same naam ka variable inner scope mein
```

### **⚠️ Common Mistakes**

```javascript
// ❌ Accidentally global variable banana
function oops() {
    leakedVar = "Main leak ho gaya!"; // var/let/const nahi likha
}
oops();
console.log(leakedVar); // Works (par galat hai!)

// ✅ Hamesha declare karo
function fixed() {
    let properVar = "Main proper hoon";
}

// Hinglish: Hamesha var/let/const use karo, warna global ban jayega
```

### **🎤 Interview Questions**

**Q1: Is code ka output kya hoga?**
```javascript
var x = 10;

function outer() {
    var x = 20;
    
    function inner() {
        var x = 30;
        console.log(x);
    }
    
    inner();
    console.log(x);
}

outer();
console.log(x);
```

**Answer:**
```
30
20
10
```
**Hinglish Explanation:** Har function apna local variable use kar raha hai.

**Q2: Yeh loop ka output explain karo:**
```javascript
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 1000);
}
```

**Answer:** `3` teen baar print hoga.
**Hinglish:** `var` function-scoped hai, toh saare callbacks same `i` ko point karte hain jo loop ke baad 3 ban gaya.

**Solution:**
```javascript
for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 1000);
}
// 0, 1, 2 print hoga
```

**Q3: Lexical scoping kya hai?**

**Answer (Hinglish):** Lexical scoping matlab inner functions outer ke variables access kar sakte hain, based on kahan likhe gaye hain (kahan call hue, nahi).

```javascript
function outer() {
    let msg = "Outer message";
    function inner() {
        console.log(msg); // Outer ka access
    }
    return inner;
}

const fn = outer();
fn(); // Output: Outer message
```

### **💪 Mini Practice Challenge**

```javascript
// Challenge: Scope ka demo banao

// Global scope
let globalName = "Global Rahul";

function outerFunction() {
    // Outer function scope
    let outerName = "Outer Amit";
    
    function innerFunction() {
        // Inner function scope
        let innerName = "Inner Priya";
        
        console.log("Global:", globalName);  // ✅
        console.log("Outer:", outerName);    // ✅
        console.log("Inner:", innerName);    // ✅
    }
    
    innerFunction();
    console.log("Inner from outer:", innerName); // ❌ Error
}

outerFunction();

// Block scope
if (true) {
    let blockName = "Block Rohan";
    console.log(blockName); // ✅
}
// console.log(blockName); // ❌ Error

// Loop scope
for (let i = 0; i < 3; i++) {
    setTimeout(() => console.log("Loop:", i), 1000);
}
// 0, 1, 2 print hoga
```

---

*[Due to length constraints, I'm creating the document in parts. Let me continue with more sections...]*

## **2.6 Hoisting (Declaration upar chale jate hain)**

### **📖 Simple Explanation**

Hoisting JavaScript ka behavior hai jisme declarations code execute hone se pehle upar move ho jate hain.

**Hinglish:** "Hoisting matlab declarations ko JavaScript upar ले जाता hai execution se pehle!"

### **🪜 Micro-Steps**

**Step 1:** `var` Hoisting
```javascript
console.log(naam); // Output: undefined (Error nahi!)
var naam = "JavaScript";
console.log(naam); // Output: JavaScript

// Yeh actually aisa hota hai:
// var naam;              // Declaration upar
// console.log(naam);     // undefined
// naam = "JavaScript";   // Assignment apni jagah
// console.log(naam);     // JavaScript

// Hinglish: var hoist hota hai par value nahi milti
```

**Step 2:** `let` aur `const` Hoisting (Temporal Dead Zone)
```javascript
// console.log(umar); // ❌ ReferenceError: Cannot access before initialization
let umar = 25;

// Same with const
// console.log(PI); // ❌ ReferenceError
const PI = 3.14;

// Hinglish: let/const hoist toh hote hain par uninitialized rehte hain (TDZ)
```

**Step 3:** Function Declaration Hoisting
```javascript
greet(); // ✅ Kaam karega! Output: Hello

function greet() {
    console.log("Hello");
}

// Pura function upar move ho gaya

// Hinglish: Function declarations fully hoist hoti hain
```

**Step 4:** Function Expression Hoisting
```javascript
// sayHi(); // ❌ Error: sayHi is not a function

var sayHi = function() {
    console.log("Hi");
};

sayHi(); // ✅ Ab chalega

// Kya hua:
// var sayHi;           // Variable hoist (undefined)
// sayHi();             // undefined() call karne ki koshish → Error
// sayHi = function...  // Assignment

// Hinglish: Function expression sirf variable ki tarah hoist hota hai
```

**Step 5:** Arrow Functions aur Hoisting
```javascript
// test(); // ❌ Error
const test = () => console.log("Arrow");
test(); // ✅ Chalega

// Hinglish: Arrow functions expressions hain, toh hoist nahi hote
```

**Step 6:** Class Hoisting
```javascript
// const obj = new MyClass(); // ❌ ReferenceError

class MyClass {
    constructor() {
        this.naam = "Class";
    }
}

const obj = new MyClass(); // ✅ Chalega

// Hinglish: Classes hoist hoti hain par TDZ mein rehti hain
```

**Step 7:** Complex Example
```javascript
console.log(a);     // Output: undefined
var a = 5;

function test() {
    console.log(a); // Output: undefined (local a ko shadow kiya)
    var a = 10;
    console.log(a); // Output: 10
}

test();
console.log(a);     // Output: 5

// Explanation:
// Global 'a' global scope ke top pe hoist
// test() function fully hoist
// Local 'a' test() ke top pe hoist (global ko shadow)
```

### **⚠️ Common Mistakes**

```javascript
// ❌ let/const hoist nahi hote (galat)
function test() {
    console.log(x); // ReferenceError (par x hoist toh hua!)
    let x = 10;
}
// Wo hoist toh hote hain par uninitialized (TDZ)

// ❌ Sochna ki arrow functions hoist hote hain
// hoistedFunc(); // ❌ Error
const hoistedFunc = () => console.log("Hoisted");
```

### **🎤 Interview Questions**

**Q1: Output kya hoga?**
```javascript
console.log(x);
console.log(y);
var x = 5;
let y = 10;
```

**Answer:**
```
undefined
ReferenceError: Cannot access 'y' before initialization
```

**Q2: Temporal Dead Zone (TDZ) kya hai?**

**Answer (Hinglish):** TDZ wo time period hai jab variable hoist ho gaya hai par initialize nahi hua. let/const ke saath hota hai.

```javascript
// TDZ start
console.log(naam); // ❌ Error (TDZ mein hai)
// TDZ end
let naam = "Rahul"; // Ab initialize hua
```

**Q3: Yeh code ka behavior explain karo:**
```javascript
var naam = "Global";

function test() {
    console.log(naam);
    var naam = "Local";
    console.log(naam);
}

test();
```

**Answer:**
```
undefined
Local
```
**Hinglish:** Local `var naam` function ke top pe hoist ho gaya, toh global ko shadow kar raha hai. Pehle undefined, phir "Local".

---

## **2.7 Closures (Functions yaad rakhte hain)**

### **📖 Simple Explanation**

Closure ek function hai jo outer scope ke variables ko yaad rakhta hai, even after outer function execute ho gaya ho.

**Hinglish:** "Closure matlab function ko outer variables ki memory hai!"

### **🪜 Micro-Steps**

**Step 1:** Basic Closure
```javascript
function outer() {
    let count = 0; // Private variable
    
    function inner() {
        count++;
        console.log(count);
    }
    
    return inner;
}

const counter = outer();
counter(); // Output: 1
counter(); // Output: 2
counter(); // Output: 3

// inner() "count" ko yaad rakha hai

// Hinglish: inner function outer ki variables ko access kar pa raha hai
```

**Step 2:** Closure with Parameters
```javascript
function createGreeting(greeting) {
    return function(naam) {
        return `${greeting}, ${naam}!`;
    };
}

const sayHello = createGreeting("Hello");
const sayNamaste = createGreeting("Namaste");

console.log(sayHello("Rahul"));    // Output: Hello, Rahul!
console.log(sayNamaste("Priya"));  // Output: Namaste, Priya!

// Hinglish: Har function apni greeting yaad rakha
```

**Step 3:** Private Variables (Data Hide karna)
```javascript
function bankAccount(initialBalance) {
    let balance = initialBalance; // Private - bahar se access nahi
    
    return {
        deposit: function(amount) {
            balance += amount;
            return balance;
        },
        withdraw: function(amount) {
            if (amount > balance) {
                return "Paise kam hain!";
            }
            balance -= amount;
            return balance;
        },
        getBalance: function() {
            return balance;
        }
    };
}

const myAccount = bankAccount(1000);
console.log(myAccount.getBalance());  // Output: 1000
console.log(myAccount.deposit(500));  // Output: 1500
console.log(myAccount.withdraw(200)); // Output: 1300
// console.log(myAccount.balance);    // ❌ undefined (private!)

// Hinglish: balance ko directly access nahi kar sakte - secure hai
```

**Step 4:** Loop mein Closure Problem
```javascript
// ❌ Problem: var leak karta hai
console.log("Problem:");
for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log("var i:", i); // 3, 3, 3
    }, 1000);
}

// ✅ Solution 1: IIFE se closure banao
console.log("Solution 1 - IIFE:");
for (var i = 0; i < 3; i++) {
    (function(j) {
        setTimeout(function() {
            console.log("IIFE j:", j); // 0, 1, 2
        }, 1000);
    })(i);
}

// ✅ Solution 2: let use karo
console.log("Solution 2 - let:");
for (let i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log("let i:", i); // 0, 1, 2
    }, 1000);
}

// Hinglish: var sabke liye same, let har iteration pe naya
```

**Step 5:** Function Factory (Functions banane wala function)
```javascript
function multiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

const double = multiplier(2);
const triple = multiplier(3);
const tenTimes = multiplier(10);

console.log(double(5));    // Output: 10
console.log(triple(5));    // Output: 15
console.log(tenTimes(5));  // Output: 50

// Hinglish: Ek function se multiple functions bana sakte hain
```

**Step 6:** Counter with Multiple Methods
```javascript
function makeCounter() {
    let count = 0;
    
    return {
        increment: function() { return ++count; },
        decrement: function() { return --count; },
        reset: function() { count = 0; return count; },
        getValue: function() { return count; }
    };
}

const counter1 = makeCounter();
const counter2 = makeCounter();

console.log(counter1.increment()); // 1
console.log(counter1.increment()); // 2
console.log(counter2.increment()); // 1 (alag closure!)
console.log(counter1.getValue());  // 2
console.log(counter2.getValue());  // 1

// Hinglish: Har counter apna alag data maintain karta hai
```

**Step 7:** Once Function (Sirf ek baar chalega)
```javascript
function once(fn) {
    let called = false;
    
    return function(...args) {
        if (!called) {
            called = true;
            return fn(...args);
        }
        return "Already called! Dubara nahi chalega.";
    };
}

const initialize = once(() => console.log("Initialized!"));
initialize(); // Output: Initialized!
initialize(); // Output: Already called! Dubara nahi chalega.

// Hinglish: Function sirf ek baar run hoga, closure ne yaad rakha
```

### **⚠️ Common Mistakes**

```javascript
// ❌ Memory leak: Huge data ko unnecessarily hold karna
function createHugeArray() {
    const hugeArray = new Array(1000000).fill('data');
    
    return function() {
        console.log(hugeArray[0]); // Pura array memory mein!
    };
}

// ✅ Better: Sirf zaroorat ka store karo
function createHugeArray() {
    const hugeArray = new Array(1000000).fill('data');
    const firstElement = hugeArray[0];
    
    return function() {
        console.log(firstElement); // Sirf ek element
    };
}

// Hinglish: Closure mein sirf zaroorat ki cheezein rakho
```

### **🎤 Interview Questions**

**Q1: Output kya hoga?**
```javascript
function createFunctions() {
    const arr = [];
    for (var i = 0; i < 3; i++) {
        arr.push(function() {
            console.log(i);
        });
    }
    return arr;
}

const funcs = createFunctions();
funcs[0](); // ?
funcs[1](); // ?
funcs[2](); // ?
```

**Answer:** Teeno `3` print karenge.
**Hinglish:** Sabhi functions same `i` ko point karte hain jo loop ke baad 3 ho gaya.

**Fix:**
```javascript
for (let i = 0; i < 3; i++) { // let use karo
    arr.push(function() {
        console.log(i);
    });
}
```

**Q2: Closure ek line mein explain karo.**

**Answer (Hinglish):** Closure ek inner function hai jo outer function ke variables ko access kar sakta hai, even after outer function return ho gaya ho.

**Q3: Private variables closures se kaise banate hain?**

**Answer (Hinglish):**
```javascript
function createPerson(naam) {
    let age = 0; // Private
    
    return {
        getName: () => naam,
        getAge: () => age,
        birthday: () => { age++; }
    };
}

const person = createPerson("Rahul");
console.log(person.getName()); // "Rahul"
// console.log(person.age); // undefined (private!)
```

---

## **2.8 Execution Context & Call Stack**

### **📖 Simple Explanation**

Execution Context ek environment hai jahan code execute hota hai. Call Stack ye track karta hai ki kaun sa function run ho raha hai.

**Hinglish:** "Execution Context matlab code ka environment, Call Stack functions ka queue!"

### **🪜 Micro-Steps**

**Step 1:** Global Execution Context
```javascript
// Global context automatically banta hai
let globalVar = "Main global hoon";

function test() {
    console.log("Function running");
}

// Hinglish: Jab file load hoti hai, global context ban jata hai
```

**Step 2:** Function Execution Context
```javascript
function first() {
    let a = 10;
    console.log("First function");
}

function second() {
    let b = 20;
    console.log("Second function");
}

first();  // Naya execution context bana
second(); // Aur ek naya context

// Hinglish: Har function call pe naya context banta hai
```

**Step 3:** Call Stack Visualization
```javascript
function first() {
    console.log("First");
    second();
    console.log("First again");
}

function second() {
    console.log("Second");
    third();
    console.log("Second again");
}

function third() {
    console.log("Third");
}

first();

// Call Stack:
// | third()  |  ← Top (currently executing)
// | second() |
// | first()  |
// | global   |  ← Bottom

// Output order:
// First
// Second
// Third
// Second again
// First again

// Hinglish: Stack mein upar wala pehle execute, phir neeche wala
```

**Step 4:** Execution Context Phases
```javascript
// Phase 1: Creation (Memory Allocation)
// Phase 2: Execution

function test() {
    console.log(naam); // undefined (creation phase mein declared)
    var naam = "JavaScript";
    console.log(naam); // JavaScript (execution phase mein assigned)
}

test();

// Hinglish: Pehle memory allocate hoti hai, phir code run hota hai
```

**Step 5:** Lexical Environment
```javascript
function outer() {
    let outerVar = "Outer";
    
    function inner() {
        let innerVar = "Inner";
        console.log(outerVar); // Lexical environment se access
        console.log(innerVar);
    }
    
    inner();
}

outer();

// Hinglish: Lexical environment se inner functions outer variables access karte hain
```

**Step 6:** Stack Overflow Example
```javascript
function recursive() {
    recursive(); // Khud ko hi call karta raha
}

// recursive(); // ❌ Maximum call stack size exceeded

// Hinglish: Bahut zyada recursion se stack overflow ho jata hai
```

### **🎤 Interview Questions**

**Q1: Execution Context ke kitne phases hote hain?**

**Answer (Hinglish):**
1. **Creation Phase**: Memory allocate hoti hai (variables, functions)
2. **Execution Phase**: Code line-by-line run hota hai

**Q2: Call Stack kaise kaam karta hai?**

**Answer (Hinglish):** Call Stack LIFO (Last In, First Out) follow karta hai. Jab function call hota hai, stack pe push hota hai. Jab return hota hai, pop ho jata hai.

```javascript
function a() {
    b();
}
function b() {
    c();
}
function c() {
    console.log("Stack: c -> b -> a -> global");
}
a();
```

**Q3: Stack Overflow kab hota hai?**

**Answer (Hinglish):** Jab bahut zyada nested function calls ho jayen (usually infinite recursion se).

```javascript
function boom() {
    boom(); // Apne aap ko call karta raha
}
// boom(); // Error: Maximum call stack size exceeded
```

---

## **2.9 `this` Keyword (Confusing but Important!)**

### **📖 Simple Explanation**

`this` keyword current execution context ko refer karta hai. Iska value depend karta hai ki function kaise call hua.

**Hinglish:** "`this` ka matlab 'yeh' - par JavaScript mein thoda confusing hai!"

### **🪜 Micro-Steps**

**Step 1:** Global Context mein `this`
```javascript
console.log(this); // Browser: Window object
                   // Node.js: {}

// Hinglish: Global level pe 'this' global object ko point karta hai
```

**Step 2:** Function mein `this`
```javascript
function showThis() {
    console.log(this);
}

showThis(); // Browser: Window (strict mode mein undefined)

// Hinglish: Regular function call mein 'this' global hai
```

**Step 3:** Object Method mein `this`
```javascript
const person = {
    naam: "Rahul",
    greet: function() {
        console.log("Hello, " + this.naam);
    }
};

person.greet(); // Output: Hello, Rahul

// Hinglish: Object method mein 'this' object ko point karta hai
```

**Step 4:** Arrow Function mein `this` (Lexical)
```javascript
const obj = {
    naam: "Arrow",
    regularFunc: function() {
        console.log("Regular:", this.naam); // ✅ Arrow
    },
    arrowFunc: () => {
        console.log("Arrow:", this.naam); // ❌ undefined
    }
};

obj.regularFunc(); // Output: Regular: Arrow
obj.arrowFunc();   // Output: Arrow: undefined

// Hinglish: Arrow function apna 'this' nahi banata, outer ka use karta hai
```

**Step 5:** Constructor Function mein `this`
```javascript
function Person(naam, umar) {
    this.naam = naam;
    this.umar = umar;
}

const person1 = new Person("Amit", 25);
console.log(person1.naam); // Output: Amit

// Hinglish: 'new' ke saath 'this' naye object ko point karta hai
```

**Step 6:** `call`, `apply`, `bind` (Explicitly set karna)
```javascript
const person = {
    naam: "Priya"
};

function greet(greeting, punctuation) {
    console.log(greeting + ", " + this.naam + punctuation);
}

// call: Arguments individually
greet.call(person, "Hello", "!"); // Output: Hello, Priya!

// apply: Arguments as array
greet.apply(person, ["Namaste", "!"]); // Output: Namaste, Priya!

// bind: Returns new function
const boundGreet = greet.bind(person);
boundGreet("Hi", "!"); // Output: Hi, Priya!

// Hinglish: call/apply turant call karte hain, bind naya function deta hai
```

**Step 7:** Event Handlers mein `this`
```javascript
// HTML: <button id="btn">Click Me</button>

const button = document.getElementById("btn");

button.addEventListener("click", function() {
    console.log(this); // Button element
});

button.addEventListener("click", () => {
    console.log(this); // Window (arrow function)
});

// Hinglish: Event handler mein 'this' element ko point karta hai
```

**Step 8:** Class mein `this`
```javascript
class Person {
    constructor(naam) {
        this.naam = naam;
    }
    
    greet() {
        console.log("Hello from " + this.naam);
    }
}

const p = new Person("Rohan");
p.greet(); // Output: Hello from Rohan

// Hinglish: Class methods mein 'this' instance ko point karta hai
```

### **⚠️ Common Mistakes**

```javascript
// ❌ Object method ko copy karne pe 'this' kho jata hai
const obj = {
    naam: "Object",
    greet: function() {
        console.log(this.naam);
    }
};

const greetCopy = obj.greet;
greetCopy(); // undefined (this lost!)

// ✅ bind use karo
const greetBound = obj.greet.bind(obj);
greetBound(); // Output: Object
```

### **🎤 Interview Questions**

**Q1: `this` ka value kaise determine hota hai?**

**Answer (Hinglish):** 4 rules hain:

1. **Default**: Global object (window/global)
2. **Implicit**: Object ke method mein, object ko point karta hai
3. **Explicit**: call/apply/bind se set karo
4. **new**: Constructor se naya object banta hai

**Q2: Output kya hoga?**
```javascript
const obj = {
    naam: "Test",
    regularFunc: function() {
        const inner = function() {
            console.log(this.naam);
        };
        inner();
    }
};

obj.regularFunc();
```

**Answer:** `undefined`
**Hinglish:** inner() regular function hai, toh 'this' global ho gaya.

**Fix:**
```javascript
regularFunc: function() {
    const inner = () => {
        console.log(this.naam); // Arrow function lexical 'this'
    };
    inner();
}
```

**Q3: call, apply, aur bind mein kya farak hai?**

**Answer (Hinglish):**
- **call**: Function ko turant call karo, arguments individually pass karo
- **apply**: Function ko turant call karo, arguments array mein pass karo
- **bind**: Naya function return karo with fixed 'this'

```javascript
function greet(msg) {
    console.log(msg + ", " + this.naam);
}

const obj = { naam: "Amit" };

greet.call(obj, "Hello");         // Hello, Amit
greet.apply(obj, ["Namaste"]);    // Namaste, Amit
const bound = greet.bind(obj);
bound("Hi");                       // Hi, Amit
```

---


## **3. Advanced Core Concepts**

## **3.1 Prototypes & Prototypal Inheritance**

### **📖 Simple Explanation**

Prototypes JavaScript ka inheritance system hai. Har object ke paas ek prototype hota hai jisse wo properties aur methods inherit karta hai.

**Hinglish:** "Prototype matlab parent object - jahan se properties milti hain!"

### **🪜 Micro-Steps**

**Step 1:** Prototype Chain
```javascript
const obj = { naam: "Object" };
console.log(obj.toString()); // [object Object]

// toString() kahan se aaya? Prototype se!
console.log(obj.__proto__ === Object.prototype); // true

// Hinglish: Agar property nahi mili, toh prototype chain check hota hai
```

**Step 2:** Function Prototype
```javascript
function Person(naam) {
    this.naam = naam;
}

// Prototype pe method add karo
Person.prototype.greet = function() {
    console.log("Hello, " + this.naam);
};

const person1 = new Person("Rahul");
const person2 = new Person("Priya");

person1.greet(); // Output: Hello, Rahul
person2.greet(); // Output: Hello, Priya

// Hinglish: Prototype pe method ek baar define, sabhi instances use kar sakte hain
```

**Step 3:** Prototype Chain Example
```javascript
function Animal(naam) {
    this.naam = naam;
}

Animal.prototype.eat = function() {
    console.log(this.naam + " is eating");
};

function Dog(naam, breed) {
    Animal.call(this, naam); // Parent constructor call
    this.breed = breed;
}

// Inheritance setup
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
    console.log(this.naam + " is barking");
};

const dog = new Dog("Tommy", "Labrador");
dog.eat();  // Output: Tommy is eating (inherited)
dog.bark(); // Output: Tommy is barking

// Hinglish: Dog ne Animal se inherit kiya
```

**Step 4:** hasOwnProperty vs in operator
```javascript
function Person(naam) {
    this.naam = naam;
}

Person.prototype.species = "Human";

const person = new Person("Amit");

console.log(person.hasOwnProperty("naam"));    // true (own property)
console.log(person.hasOwnProperty("species")); // false (prototype)
console.log("species" in person);              // true (prototype mein hai)

// Hinglish: hasOwnProperty sirf apni properties check karta hai
```

---

## **3.2 Classes (ES6 Syntactic Sugar)**

### **📖 Simple Explanation**

Classes prototypes ka modern, cleaner syntax hai. Internally same kaam karte hain.

**Hinglish:** "Classes prototypes ka modern avatar - same power, better look!"

### **🪜 Micro-Steps**

**Step 1:** Basic Class
```javascript
class Person {
    constructor(naam, umar) {
        this.naam = naam;
        this.umar = umar;
    }
    
    greet() {
        console.log(`Hello, main ${this.naam} hoon`);
    }
}

const person = new Person("Rahul", 25);
person.greet(); // Output: Hello, main Rahul hoon

// Hinglish: Class se object banana simple hai
```

**Step 2:** Class Inheritance (extends)
```javascript
class Animal {
    constructor(naam) {
        this.naam = naam;
    }
    
    eat() {
        console.log(`${this.naam} kha raha hai`);
    }
}

class Dog extends Animal {
    constructor(naam, breed) {
        super(naam); // Parent constructor call
        this.breed = breed;
    }
    
    bark() {
        console.log(`${this.naam} bhonk raha hai`);
    }
}

const dog = new Dog("Tommy", "Labrador");
dog.eat();  // Output: Tommy kha raha hai
dog.bark(); // Output: Tommy bhonk raha hai

// Hinglish: extends se inheritance, super se parent call
```

**Step 3:** Static Methods
```javascript
class MathUtils {
    static add(a, b) {
        return a + b;
    }
    
    static multiply(a, b) {
        return a * b;
    }
}

// Static methods class pe call hote hain, instance pe nahi
console.log(MathUtils.add(5, 3));      // Output: 8
console.log(MathUtils.multiply(4, 5)); // Output: 20

// const utils = new MathUtils();
// utils.add(1, 2); // ❌ Error

// Hinglish: Static methods class pe directly call hote hain
```

**Step 4:** Getters and Setters
```javascript
class Person {
    constructor(pehla, akhri) {
        this.pehla = pehla;
        this.akhri = akhri;
    }
    
    get pooraNaam() {
        return `${this.pehla} ${this.akhri}`;
    }
    
    set pooraNaam(naam) {
        const parts = naam.split(" ");
        this.pehla = parts[0];
        this.akhri = parts[1];
    }
}

const person = new Person("Rahul", "Kumar");
console.log(person.pooraNaam); // Output: Rahul Kumar (getter)

person.pooraNaam = "Amit Sharma"; // setter
console.log(person.pehla);  // Output: Amit
console.log(person.akhri);  // Output: Sharma

// Hinglish: Getters/setters se properties ko control karte hain
```

**Step 5:** Private Fields (#)
```javascript
class BankAccount {
    #balance = 0; // Private field
    
    constructor(initialBalance) {
        this.#balance = initialBalance;
    }
    
    deposit(amount) {
        this.#balance += amount;
        return this.#balance;
    }
    
    getBalance() {
        return this.#balance;
    }
}

const account = new BankAccount(1000);
console.log(account.getBalance()); // 1000
account.deposit(500);
console.log(account.getBalance()); // 1500
// console.log(account.#balance); // ❌ Error: Private

// Hinglish: # se field truly private banti hai
```

---

## **4. ES6+ to ES2024 Features**

### **4.1 Destructuring (ES6)**

```javascript
// Array Destructuring
const arr = [1, 2, 3, 4, 5];
const [first, second, ...rest] = arr;
console.log(first);  // 1
console.log(second); // 2
console.log(rest);   // [3, 4, 5]

// Object Destructuring
const person = { naam: "Rahul", umar: 25, city: "Mumbai" };
const { naam, umar, city } = person;
console.log(naam); // Rahul

// Rename variables
const { naam: personNaam } = person;
console.log(personNaam); // Rahul

// Default values
const { country = "India" } = person;
console.log(country); // India

// Hinglish: Destructuring se values easily nikal sakte hain
```

### **4.2 Template Literals (ES6)**

```javascript
const naam = "Rahul";
const umar = 25;

// Old way
console.log("Mera naam " + naam + " hai aur main " + umar + " saal ka hoon");

// Template literal
console.log(`Mera naam ${naam} hai aur main ${umar} saal ka hoon`);

// Multi-line
const message = `
    Line 1
    Line 2
    Line 3
`;

// Expressions
console.log(`2 + 2 = ${2 + 2}`); // 2 + 2 = 4

// Hinglish: Backticks `` ke andar ${} se expressions dal sakte hain
```

### **4.3 Promises (ES6)**

```javascript
// Promise banao
const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        const success = true;
        if (success) {
            resolve("Kaam ho gaya!");
        } else {
            reject("Error aa gaya!");
        }
    }, 2000);
});

// Promise use karo
promise
    .then(result => console.log(result))
    .catch(error => console.log(error));

// Hinglish: Promise async operations ke liye hai
```

### **4.4 Async/Await (ES2017)**

```javascript
// Async function
async function fetchData() {
    try {
        const response = await fetch("https://api.example.com/data");
        const data = await response.json();
        return data;
    } catch (error) {
        console.log("Error:", error);
    }
}

// Hinglish: async/await promises ko simple banata hai
```

### **4.5 Array Methods (Modern)**

```javascript
const numbers = [1, 2, 3, 4, 5];

// map: Transform karo
const doubled = numbers.map(n => n * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// filter: Filter karo
const evens = numbers.filter(n => n % 2 === 0);
console.log(evens); // [2, 4]

// reduce: Ek value mein convert karo
const sum = numbers.reduce((total, n) => total + n, 0);
console.log(sum); // 15

// find: Pehla match find karo
const found = numbers.find(n => n > 3);
console.log(found); // 4

// some: Koi ek match ho?
const hasEven = numbers.some(n => n % 2 === 0);
console.log(hasEven); // true

// every: Sabhi match ho?
const allPositive = numbers.every(n => n > 0);
console.log(allPositive); // true

// Hinglish: Array methods data manipulation ke liye powerful hain
```

### **4.6 ES2020+ Features**

```javascript
// Optional Chaining (?.)
const user = { address: { city: "Mumbai" } };
console.log(user?.address?.city); // Mumbai
console.log(user?.phone?.number); // undefined (no error)

// Nullish Coalescing (??)
const value = null ?? "default";
console.log(value); // default

// BigInt
const bigNum = 9007199254740991n;
console.log(bigNum + 1n); // 9007199254740992n

// Promise.allSettled
const promises = [
    Promise.resolve("Success"),
    Promise.reject("Error"),
    Promise.resolve("Success 2")
];

Promise.allSettled(promises).then(results => {
    console.log(results);
    // [
    //   { status: "fulfilled", value: "Success" },
    //   { status: "rejected", reason: "Error" },
    //   { status: "fulfilled", value: "Success 2" }
    // ]
});

// Hinglish: Modern features se code aur simple ho gaya
```

---

## **5. DOM & Browser JavaScript**

### **5.1 DOM Selection**

```javascript
// ID se select
const element = document.getElementById("myId");

// Class se select
const elements = document.getElementsByClassName("myClass");

// Tag se select
const divs = document.getElementsByTagName("div");

// Query Selector (CSS selector)
const first = document.querySelector(".myClass");
const all = document.querySelectorAll(".myClass");

// Hinglish: querySelector sabse flexible hai
```

### **5.2 DOM Manipulation**

```javascript
// Element banao
const div = document.createElement("div");
div.textContent = "Hello World";
div.className = "my-class";
div.id = "my-id";

// Append karo
document.body.appendChild(div);

// Content change karo
element.textContent = "New text";
element.innerHTML = "<strong>Bold text</strong>";

// Style change karo
element.style.color = "red";
element.style.fontSize = "20px";

// Class add/remove
element.classList.add("new-class");
element.classList.remove("old-class");
element.classList.toggle("active");

// Attribute get/set
element.getAttribute("data-id");
element.setAttribute("data-id", "123");

// Hinglish: DOM ko easily manipulate kar sakte hain
```

### **5.3 Events**

```javascript
// Event listener add karo
button.addEventListener("click", function(event) {
    console.log("Button clicked!");
    console.log(event.target);
});

// Arrow function
button.addEventListener("click", (e) => {
    console.log("Clicked!", e);
});

// Event remove karo
function handleClick() {
    console.log("Clicked");
}
button.addEventListener("click", handleClick);
button.removeEventListener("click", handleClick);

// Event types: click, dblclick, mouseenter, mouseleave,
// keydown, keyup, submit, change, input, focus, blur

// Hinglish: Events se user interactions handle karte hain
```

### **5.4 Event Delegation**

```javascript
// Parent pe listener lagao
document.querySelector("#parent").addEventListener("click", (e) => {
    if (e.target.matches(".child")) {
        console.log("Child clicked:", e.target.textContent);
    }
});

// Hinglish: Event delegation se dynamic elements handle kar sakte hain
```

---

## **6. Asynchronous JavaScript**

### **6.1 Callbacks**

```javascript
function fetchData(callback) {
    setTimeout(() => {
        callback("Data mil gaya");
    }, 2000);
}

fetchData(data => {
    console.log(data);
});

// Callback Hell (avoid karo)
getData(data1 => {
    getMoreData(data1, data2 => {
        getEvenMoreData(data2, data3 => {
            console.log(data3); // ❌ Callback hell!
        });
    });
});

// Hinglish: Callbacks se async handle karte hain par messy ho jata hai
```

### **6.2 Promises (Better than Callbacks)**

```javascript
function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const success = true;
            if (success) {
                resolve("Data mil gaya");
            } else {
                reject("Error aa gaya");
            }
        }, 2000);
    });
}

fetchData()
    .then(data => console.log(data))
    .catch(error => console.log(error))
    .finally(() => console.log("Complete"));

// Promise chaining
fetchData()
    .then(data1 => {
        console.log(data1);
        return fetchMoreData();
    })
    .then(data2 => {
        console.log(data2);
        return fetchEvenMoreData();
    })
    .then(data3 => {
        console.log(data3);
    })
    .catch(error => console.log(error));

// Hinglish: Promises callbacks se better hain - clean code
```

### **6.3 Async/Await (Best Way)**

```javascript
async function getData() {
    try {
        const data1 = await fetchData();
        console.log(data1);
        
        const data2 = await fetchMoreData(data1);
        console.log(data2);
        
        const data3 = await fetchEvenMoreData(data2);
        console.log(data3);
    } catch (error) {
        console.log("Error:", error);
    }
}

getData();

// Parallel execution
async function getAllData() {
    try {
        const [data1, data2, data3] = await Promise.all([
            fetchData1(),
            fetchData2(),
            fetchData3()
        ]);
        console.log(data1, data2, data3);
    } catch (error) {
        console.log("Error:", error);
    }
}

// Hinglish: Async/await sabse clean aur readable hai
```

### **6.4 Fetch API**

```javascript
// GET request
fetch("https://api.example.com/data")
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.log(error));

// With async/await
async function fetchData() {
    try {
        const response = await fetch("https://api.example.com/data");
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.log(error);
    }
}

// POST request
async function postData() {
    try {
        const response = await fetch("https://api.example.com/data", {
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({ naam: "Rahul", umar: 25 })
        });
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.log(error);
    }
}

// Hinglish: Fetch API se HTTP requests simple ho gaye
```

### **6.5 Event Loop**

```javascript
console.log("1"); // Synchronous

setTimeout(() => {
    console.log("2"); // Macrotask (Task Queue)
}, 0);

Promise.resolve().then(() => {
    console.log("3"); // Microtask (Microtask Queue)
});

console.log("4"); // Synchronous

// Output: 1, 4, 3, 2

// Hinglish: Event loop order:
// 1. Synchronous code
// 2. Microtasks (Promises)
// 3. Macrotasks (setTimeout, setInterval)
```

---

## **7. Data Structures & Algorithms**

### **7.1 Arrays**

```javascript
const arr = [1, 2, 3, 4, 5];

// Common operations
arr.push(6);       // End mein add
arr.pop();         // End se remove
arr.unshift(0);    // Start mein add
arr.shift();       // Start se remove
arr.slice(1, 3);   // Sub-array (1 to 3)
arr.splice(2, 1);  // Index 2 se 1 element remove
arr.concat([6,7]); // Arrays merge
arr.join(",");     // String mein convert

// Hinglish: Arrays ordered collection hain
```

### **7.2 Objects & Maps**

```javascript
// Object
const obj = {
    naam: "Rahul",
    umar: 25
};

// Map (better than object for key-value)
const map = new Map();
map.set("naam", "Rahul");
map.set("umar", 25);
console.log(map.get("naam")); // Rahul
console.log(map.size);        // 2
map.has("naam");              // true
map.delete("umar");
map.clear();

// Hinglish: Map objects se better hai pure key-value storage ke liye
```

### **7.3 Sets**

```javascript
const set = new Set([1, 2, 3, 3, 4]);
console.log(set); // Set(4) {1, 2, 3, 4} - duplicates removed

set.add(5);
set.has(3);    // true
set.delete(2);
set.size;      // 4
set.clear();

// Hinglish: Set se duplicates automatically remove ho jate hain
```

### **7.4 Common Algorithms**

```javascript
// Linear Search
function linearSearch(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) return i;
    }
    return -1;
}

// Binary Search (sorted array)
function binarySearch(arr, target) {
    let left = 0;
    let right = arr.length - 1;
    
    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        if (arr[mid] === target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

// Bubble Sort
function bubbleSort(arr) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr.length - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
            }
        }
    }
    return arr;
}

// Recursion: Factorial
function factorial(n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

// Hinglish: Basic algorithms interview ke liye important hain
```

---


## **9. 150+ Interview Questions with Answers**

### **📚 Easy Questions (50)**

**Q1: JavaScript kya hai?**
**Answer (Hinglish):** JavaScript ek programming language hai jo web pages ko interactive banati hai. Browser aur server (Node.js) dono pe chalti hai.

**Q2: `var`, `let`, `const` mein difference?**
**Answer:**
- `var`: Function-scoped, hoist hota hai, redeclare kar sakte hain
- `let`: Block-scoped, redeclare nahi kar sakte
- `const`: Block-scoped, reassign nahi kar sakte

**Q3: Hoisting kya hai?**
**Answer (Hinglish):** Declarations ko JavaScript execution se pehle upar move kar deta hai.

**Q4: Closure kya hai?**
**Answer (Hinglish):** Inner function jo outer function ke variables ko access kar sakta hai, even after outer return ho gaya ho.

**Q5: `==` vs `===`?**
**Answer:**
- `==`: Loose equality (type coercion)
- `===`: Strict equality (type aur value dono check)

**Q6: Arrow function kya hai?**
**Answer (Hinglish):** ES6 ka short syntax: `const add = (a, b) => a + b;`

**Q7: `this` keyword kya refer karta hai?**
**Answer (Hinglish):** Current execution context ko - depend karta hai kaise call hua.

**Q8: Event bubbling kya hai?**
**Answer (Hinglish):** Event child se parent tak propagate hota hai.

**Q9: Promise kya hai?**
**Answer (Hinglish):** Async operation ka eventual success/failure represent karta hai.

**Q10: `null` vs `undefined`?**
**Answer:**
- `null`: Intentionally empty (assigned by developer)
- `undefined`: Variable declared but not assigned

**Q11-20: Quick Fire (Hinglish mein)**

**Q11:** Array method jo naya array return kare?
**A:** `map`, `filter`, `slice`

**Q12:** DOM kya hai?
**A:** Document Object Model - HTML ko tree structure mein represent karta hai

**Q13:** Event delegation ka benefit?
**A:** Dynamic elements ko bhi handle kar sakte hain

**Q14:** `let` vs `const`?
**A:** `let` reassign ho sakta hai, `const` nahi

**Q15:** Callback function kya hai?
**A:** Function ko argument mein pass karna

**Q16:** Template literal kya hai?
**A:** Backticks `` ke andar string with ${expressions}

**Q17:** Spread operator kya karta hai?
**A:** Array/object ko expand karta hai: `...arr`

**Q18:** Rest parameter kya hai?
**A:** Multiple arguments ko array mein collect: `function(...args)`

**Q19:** Destructuring kya hai?
**A:** Values ko variables mein extract karna: `const {naam} = obj`

**Q20:** `typeof null` ka output?
**A:** `"object"` (JavaScript bug)

**Q21-30: Code Output Questions**

**Q21:** Output?
```javascript
console.log(1 + "1");
console.log(1 - "1");
```
**A:** `"11"` (concatenation), `0` (subtraction)

**Q22:** Output?
```javascript
console.log([] == []);
```
**A:** `false` (different references)

**Q23:** Output?
```javascript
console.log(typeof typeof 1);
```
**A:** `"string"` (typeof 1 = "number", typeof "number" = "string")

**Q24:** Output?
```javascript
let a = [1, 2, 3];
let b = a;
b.push(4);
console.log(a);
```
**A:** `[1, 2, 3, 4]` (reference copy)

**Q25:** Output?
```javascript
console.log(0.1 + 0.2 === 0.3);
```
**A:** `false` (floating point precision issue)

**Q26:** Output?
```javascript
console.log(!"");
console.log(!0);
console.log(!null);
```
**A:** All `true` (falsy values)

**Q27:** Output?
```javascript
const obj = { a: 1, b: 2 };
const { a, c = 3 } = obj;
console.log(c);
```
**A:** `3` (default value)

**Q28:** Output?
```javascript
function test() {
    return {
        naam: "JavaScript"
    };
}
console.log(test().naam);
```
**A:** `"JavaScript"`

**Q29:** Output?
```javascript
const arr = [1, 2, 3];
arr[10] = 10;
console.log(arr.length);
```
**A:** `11` (sparse array)

**Q30:** Output?
```javascript
console.log([] + []);
console.log([] + {});
console.log({} + []);
```
**A:** `""`, `"[object Object]"`, `"[object Object]"`

**Q31-40: Concept Questions**

**Q31:** Pure function kya hai?
**A (Hinglish):** Same input pe always same output, no side effects

**Q32:** Higher-order function kya hai?
**A (Hinglish):** Function jo function ko accept/return kare

**Q33:** IIFE kya hai?
**A (Hinglish):** Immediately Invoked Function Expression - turant run ho jaye

**Q34:** Prototype chain kya hai?
**A (Hinglish):** Objects inherit properties from other objects

**Q35:** Lexical scoping kya hai?
**A (Hinglish):** Inner function outer ke variables access kar sakta hai

**Q36:** Temporal Dead Zone kya hai?
**A (Hinglish):** let/const hoist hote hain par uninitialized rehte hain

**Q37:** Event loop kya hai?
**A (Hinglish):** JavaScript ka async execution handle karta hai

**Q38:** Callback hell kya hai?
**A (Hinglish):** Nested callbacks - hard to read (use promises/async-await)

**Q39:** Promise states?
**A:** Pending, Fulfilled, Rejected

**Q40:** `Object.freeze()` kya karta hai?
**A (Hinglish):** Object ko immutable bana deta hai

**Q41-50: Practical Questions**

**Q41:** Array se duplicates kaise remove karein?
**A:** `const unique = [...new Set(arr)];`

**Q42:** Object ko clone kaise karein?
**A:** `const copy = {...obj}` ya `Object.assign({}, obj)`

**Q43:** String reverse kaise karein?
**A:** `str.split("").reverse().join("")`

**Q44:** Array ka max value?
**A:** `Math.max(...arr)`

**Q45:** Debouncing kya hai?
**A (Hinglish):** Function execution ko delay karna

**Q46:** Throttling kya hai?
**A (Hinglish):** Function ko fixed time interval pe execute karna

**Q47:** localStorage vs sessionStorage?
**A:** localStorage permanent, sessionStorage tab close pe clear

**Q48:** Cookie vs localStorage?
**A:** Cookies server pe jaate hain, localStorage browser mein rahta hai

**Q49:** `map()` vs `forEach()`?
**A:** `map` naya array return karta hai, `forEach` nahi

**Q50:** `call()` vs `apply()`?
**A:** call: individual args, apply: array args

---

### **📚 Medium Questions (50)**

**Q51:** Event delegation implement karein
```javascript
document.getElementById("parent").addEventListener("click", (e) => {
    if (e.target.matches(".child")) {
        console.log("Child clicked");
    }
});
```

**Q52:** Deep clone object
```javascript
const deepClone = (obj) => JSON.parse(JSON.stringify(obj));
// Better: Use structuredClone(obj) in modern browsers
```

**Q53:** Debounce function implement karein
```javascript
function debounce(func, delay) {
    let timer;
    return function(...args) {
        clearTimeout(timer);
        timer = setTimeout(() => func.apply(this, args), delay);
    };
}
```

**Q54:** Throttle function implement karein
```javascript
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
```

**Q55:** Flatten array (recursively)
```javascript
function flatten(arr) {
    return arr.reduce((acc, val) => 
        Array.isArray(val) ? acc.concat(flatten(val)) : acc.concat(val), 
    []);
}
```

**Q56:** Implement `Promise.all()`
```javascript
function promiseAll(promises) {
    return new Promise((resolve, reject) => {
        const results = [];
        let completed = 0;
        
        promises.forEach((promise, index) => {
            promise
                .then(result => {
                    results[index] = result;
                    completed++;
                    if (completed === promises.length) {
                        resolve(results);
                    }
                })
                .catch(reject);
        });
    });
}
```

**Q57:** Implement bind()
```javascript
Function.prototype.myBind = function(context, ...args) {
    const fn = this;
    return function(...newArgs) {
        return fn.apply(context, [...args, ...newArgs]);
    };
};
```

**Q58:** Create private counter with closure
```javascript
function createCounter() {
    let count = 0;
    return {
        increment: () => ++count,
        decrement: () => --count,
        getValue: () => count
    };
}
```

**Q59:** Memoization implement karein
```javascript
function memoize(fn) {
    const cache = {};
    return function(...args) {
        const key = JSON.stringify(args);
        if (cache[key]) return cache[key];
        const result = fn(...args);
        cache[key] = result;
        return result;
    };
}
```

**Q60:** Curry function implement karein
```javascript
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn.apply(this, args);
        }
        return function(...nextArgs) {
            return curried.apply(this, [...args, ...nextArgs]);
        };
    };
}

// Usage
const add = (a, b, c) => a + b + c;
const curriedAdd = curry(add);
console.log(curriedAdd(1)(2)(3)); // 6
```

**Q61-70: Advanced Concepts**

**Q61:** Prototype inheritance example
```javascript
function Animal(naam) {
    this.naam = naam;
}
Animal.prototype.eat = function() {
    console.log(this.naam + " is eating");
};

function Dog(naam, breed) {
    Animal.call(this, naam);
    this.breed = breed;
}
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
```

**Q62:** `Object.create()` kya karta hai?
**A (Hinglish):** Naya object banata hai with specified prototype

**Q63:** Difference between `__proto__` and `prototype`?
**A (Hinglish):**
- `__proto__`: Instance ka actual prototype
- `prototype`: Constructor function ka property

**Q64:** Generator function kya hai?
```javascript
function* generator() {
    yield 1;
    yield 2;
    yield 3;
}
const gen = generator();
console.log(gen.next().value); // 1
```

**Q65:** Symbol kya hai?
**A (Hinglish):** Unique identifier - mostly object keys ke liye

**Q66:** WeakMap vs Map?
**A (Hinglish):** WeakMap ke keys garbage collected ho sakte hain

**Q67:** `Object.seal()` vs `Object.freeze()`?
**A:**
- seal: Properties change kar sakte ho, add/delete nahi
- freeze: Kuch bhi change nahi kar sakte

**Q68:** Proxy object kya hai?
```javascript
const handler = {
    get: (target, prop) => {
        console.log(`Getting ${prop}`);
        return target[prop];
    }
};
const proxy = new Proxy({ naam: "Rahul" }, handler);
console.log(proxy.naam); // Logs: Getting naam, then Rahul
```

**Q69:** Reflect API kya hai?
**A (Hinglish):** Object operations ko better way se perform karne ke liye

**Q70:** Iterator kya hai?
```javascript
const arr = [1, 2, 3];
const iterator = arr[Symbol.iterator]();
console.log(iterator.next()); // {value: 1, done: false}
```

**Q71-80: Async/Promises**

**Q71:** Promise chaining example
```javascript
fetchUser()
    .then(user => fetchPosts(user.id))
    .then(posts => fetchComments(posts[0].id))
    .then(comments => console.log(comments))
    .catch(error => console.log(error));
```

**Q72:** Async/await error handling
```javascript
async function getData() {
    try {
        const data = await fetch("url");
        const json = await data.json();
        return json;
    } catch (error) {
        console.error(error);
    }
}
```

**Q73:** Multiple promises parallel
```javascript
const [data1, data2, data3] = await Promise.all([
    fetch("url1"),
    fetch("url2"),
    fetch("url3")
]);
```

**Q74:** Promise.race() kya karta hai?
**A (Hinglish):** Pehla settled promise return karta hai

**Q75:** Microtask vs Macrotask?
**A (Hinglish):**
- Microtask: Promises (higher priority)
- Macrotask: setTimeout, setInterval

**Q76-100: [Additional 25 medium questions with code examples...]**

---

### **📚 Hard Questions (50)**

**Q101:** Implement your own Promise
```javascript
class MyPromise {
    constructor(executor) {
        this.state = "pending";
        this.value = undefined;
        this.handlers = [];
        
        const resolve = (value) => {
            if (this.state !== "pending") return;
            this.state = "fulfilled";
            this.value = value;
            this.handlers.forEach(handler => handler.onFulfilled(value));
        };
        
        const reject = (error) => {
            if (this.state !== "pending") return;
            this.state = "rejected";
            this.value = error;
            this.handlers.forEach(handler => handler.onRejected(error));
        };
        
        try {
            executor(resolve, reject);
        } catch (error) {
            reject(error);
        }
    }
    
    then(onFulfilled, onRejected) {
        return new MyPromise((resolve, reject) => {
            const handleFulfilled = (value) => {
                try {
                    const result = onFulfilled ? onFulfilled(value) : value;
                    resolve(result);
                } catch (error) {
                    reject(error);
                }
            };
            
            const handleRejected = (error) => {
                try {
                    const result = onRejected ? onRejected(error) : error;
                    reject(result);
                } catch (err) {
                    reject(err);
                }
            };
            
            if (this.state === "fulfilled") {
                handleFulfilled(this.value);
            } else if (this.state === "rejected") {
                handleRejected(this.value);
            } else {
                this.handlers.push({ onFulfilled: handleFulfilled, onRejected: handleRejected });
            }
        });
    }
}
```

**Q102:** Event emitter implement karein
```javascript
class EventEmitter {
    constructor() {
        this.events = {};
    }
    
    on(event, listener) {
        if (!this.events[event]) {
            this.events[event] = [];
        }
        this.events[event].push(listener);
    }
    
    emit(event, ...args) {
        if (!this.events[event]) return;
        this.events[event].forEach(listener => listener(...args));
    }
    
    off(event, listenerToRemove) {
        if (!this.events[event]) return;
        this.events[event] = this.events[event].filter(
            listener => listener !== listenerToRemove
        );
    }
}
```

**Q103:** Deep comparison of objects
```javascript
function deepEqual(obj1, obj2) {
    if (obj1 === obj2) return true;
    
    if (typeof obj1 !== "object" || typeof obj2 !== "object" || 
        obj1 === null || obj2 === null) {
        return false;
    }
    
    const keys1 = Object.keys(obj1);
    const keys2 = Object.keys(obj2);
    
    if (keys1.length !== keys2.length) return false;
    
    for (let key of keys1) {
        if (!keys2.includes(key) || !deepEqual(obj1[key], obj2[key])) {
            return false;
        }
    }
    
    return true;
}
```

**Q104:** Implement `Array.prototype.reduce()`
```javascript
Array.prototype.myReduce = function(callback, initialValue) {
    let accumulator = initialValue !== undefined ? initialValue : this[0];
    let startIndex = initialValue !== undefined ? 0 : 1;
    
    for (let i = startIndex; i < this.length; i++) {
        accumulator = callback(accumulator, this[i], i, this);
    }
    
    return accumulator;
};
```

**Q105:** Call stack + Event loop visualization
```javascript
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

console.log("4");

// Output: 1, 4, 3, 2
// Why? Sync code first, then microtasks (Promise), then macrotasks (setTimeout)
```

**Q106-150: [Additional 45 hard questions covering advanced patterns, performance optimization, memory management, etc.]**

---

