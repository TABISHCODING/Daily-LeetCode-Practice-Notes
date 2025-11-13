# Python Backend Developer - Complete Stairwise Guide (Django + DRF)

**Hinglish Main Guide - Bilkul Beginner se Production-Ready Backend Developer tak ka Complete Journey**

## 📚 Table of Contents
1. [Introduction & Learning Path](#introduction--learning-path)
2. [Phase 1: Python Fundamentals](#phase-1-python-fundamentals)
3. [Phase 2: Web Fundamentals](#phase-2-web-fundamentals)
4. [Phase 3: Django Basics](#phase-3-django-basics)
5. [Phase 4: Django REST Framework (DRF)](#phase-4-django-rest-framework-drf)
6. [Phase 5: Testing & Debugging](#phase-5-testing--debugging)
7. [Phase 6: Security & Best Practices](#phase-6-security--best-practices)
8. [Phase 7: CI/CD & Deployment](#phase-7-cicd--deployment)
9. [Mini Projects & Capstone](#mini-projects--capstone)
10. [Interview Questions & Answers](#interview-questions--answers)
11. [Commands Cheatsheet](#commands-cheatsheet)
12. [Resources & Next Steps](#resources--next-steps)

---

## Introduction & Learning Path

**Kya seekhenge hum?**  
Is guide mein aap sikhenge kaise Python ke saath professional backend web applications aur REST APIs banaye. Django (full-featured web framework) aur Django REST Framework (API building ke liye) ko depth mein cover karenge.

**Kis tarah se seekhenge?**  
Stairwise approach - har concept ek chhoti, independent task hai jo previous task pe build karti hai. Har step mein:
- Clear explanation (plain language mein)
- Why it matters (real-world context)
- Exact commands aur code (copy-paste ready)
- Expected output
- Common pitfalls
- Interview question with answer

**Timeline (Suggested):**
- **Phase 1:** Python Basics - 1-2 weeks (agar already familiar ho)
- **Phase 2:** Web Fundamentals - 1 week
- **Phase 3:** Django Basics - 4-6 weeks
- **Phase 4:** DRF APIs - 3-4 weeks
- **Phase 5:** Testing/Debugging - 2 weeks
- **Phase 6:** Security - 1 week
- **Phase 7:** Deployment - 2 weeks
- **Total:** 14-18 weeks (3-4 months) with consistent practice

---

## Phase 1: Python Fundamentals

**Quick Refresher Checklist** (Skip karo agar comfortable ho)

### Stair 1.1: Variables, Data Types, Control Flow

**Explanation:**  
Python mein variables dynamically typed hain - koi explicit type declaration nahi chahiye. Control flow structures (if/else, loops) simple aur readable hain.

**Why it matters:**  
Django views aur API logic mein har jagah conditional logic aur loops use hote hain.

**Micro-steps:**

1. **Create a simple Python script**
```bash
mkdir -p ~/learn_python && cd ~/learn_python
touch basics.py
```

2. **Write basic Python code (basics.py):**
```python
# Variables and data types
name = "Django Developer"
age = 25
skills = ["Python", "Django", "REST APIs"]
is_learning = True

# Control flow
if is_learning:
    print(f"{name} is learning backend development")
    
# Loop through skills
for skill in skills:
    print(f"- {skill}")

# Dictionary (important for JSON/API responses)
user = {
    "username": "admin",
    "email": "admin@example.com",
    "is_active": True
}
print(f"User email: {user['email']}")
```

3. **Run the script:**
```bash
python3 basics.py
```

**Expected Output:**
```
Django Developer is learning backend development
- Python
- Django
- REST APIs
User email: admin@example.com
```

**Pitfall:**  
Indentation matters! Python uses spaces (4 spaces standard) for code blocks. Mixing tabs and spaces causes `IndentationError`.

**Interview Q:**  
*Q: Python mein dictionary kya hai aur API development mein kaise useful hai?*  
A: Dictionary ek key-value pair data structure hai. APIs mein JSON data ko represent karne ke liye dictionaries use hoti hain kyunki JSON aur Python dict ka structure similar hai. Django serializers internally dicts use karte hain.

---

### Stair 1.2: Functions, Classes & OOP

**Explanation:**  
Functions code ko reusable banate hain. Classes objects create karte hain jo data aur behavior encapsulate karte hain. Django extensively OOP use karta hai (models, views, serializers sab classes hain).

**Why it matters:**  
Django models, class-based views, aur DRF serializers sab OOP concepts pe based hain.

**Micro-steps:**

1. **Create OOP examples (oop_basics.py):**
```python
# Function example
def calculate_discount(price, discount_percent):
    """Calculate discounted price"""
    discount_amount = price * (discount_percent / 100)
    return price - discount_amount

# Class example (similar to Django models)
class Product:
    def __init__(self, name, price, stock):
        self.name = name
        self.price = price
        self.stock = stock
    
    def __str__(self):
        return f"{self.name} - ${self.price}"
    
    def is_available(self):
        return self.stock > 0
    
    def sell(self, quantity=1):
        if quantity <= self.stock:
            self.stock -= quantity
            return True
        return False

# Usage
laptop = Product("MacBook Pro", 1500, 10)
print(laptop)  # Calls __str__
print(f"Available: {laptop.is_available()}")
laptop.sell(2)
print(f"Remaining stock: {laptop.stock}")

# Inheritance (Django views use this)
class DiscountedProduct(Product):
    def __init__(self, name, price, stock, discount):
        super().__init__(name, price, stock)
        self.discount = discount
    
    def get_discounted_price(self):
        return calculate_discount(self.price, self.discount)

sale_item = DiscountedProduct("iPhone", 1000, 5, 15)
print(f"Original: ${sale_item.price}, Discounted: ${sale_item.get_discounted_price()}")
```

2. **Run:**
```bash
python3 oop_basics.py
```

**Expected Output:**
```
MacBook Pro - $1500
Available: True
Remaining stock: 8
Original: $1000, Discounted: $850.0
```

**Pitfall:**  
`__init__` mein `self` parameter hamesha pehle aana chahiye. `__str__` method string return karna chahiye, not None.

**Interview Q:**  
*Q: Django mein `__str__` method ka kya use hai?*  
A: Django admin panel aur shell mein jab model instance display hota hai, tab `__str__` method call hota hai. Ye human-readable representation provide karta hai, by default object ID ke bajaye meaningful text dikhata hai.

---

### Stair 1.3: List Comprehensions, Lambda, Map/Filter

**Explanation:**  
Python ke functional programming features jo code ko concise banate hain. Django ORM queries aur serializer validations mein frequently use hote hain.

**Why it matters:**  
Queryset manipulation, data transformation, aur filtering logic ko clean aur readable rakhne ke liye essential hai.

**Micro-steps:**

1. **Create functional programming examples (functional.py):**
```python
# List comprehension
numbers = [1, 2, 3, 4, 5]
squares = [n**2 for n in numbers]
print(f"Squares: {squares}")

# With condition (similar to filtering querysets)
even_squares = [n**2 for n in numbers if n % 2 == 0]
print(f"Even squares: {even_squares}")

# Dictionary comprehension (useful for serializing data)
users = [
    {"id": 1, "name": "Alice", "active": True},
    {"id": 2, "name": "Bob", "active": False},
    {"id": 3, "name": "Charlie", "active": True}
]

active_users = {user["id"]: user["name"] for user in users if user["active"]}
print(f"Active users: {active_users}")

# Lambda functions (for custom sorting/filtering)
products = [
    {"name": "Laptop", "price": 1000},
    {"name": "Mouse", "price": 25},
    {"name": "Keyboard", "price": 75}
]

# Sort by price
sorted_products = sorted(products, key=lambda p: p["price"])
print("\nProducts sorted by price:")
for p in sorted_products:
    print(f"  {p['name']}: ${p['price']}")

# Filter expensive items
expensive = list(filter(lambda p: p["price"] > 50, products))
print(f"\nExpensive products: {[p['name'] for p in expensive]}")

# Map - transform all items
discounted = list(map(lambda p: {**p, "price": p["price"] * 0.9}, products))
print(f"\nDiscounted prices: {[(p['name'], p['price']) for p in discounted]}")
```

2. **Run:**
```bash
python3 functional.py
```

**Expected Output:**
```
Squares: [1, 4, 9, 16, 25]
Even squares: [4, 16]
Active users: {1: 'Alice', 3: 'Charlie'}

Products sorted by price:
  Mouse: $25
  Keyboard: $75
  Laptop: $1000

Expensive products: ['Laptop', 'Keyboard']

Discounted prices: [('Laptop', 900.0), ('Mouse', 22.5), ('Keyboard', 67.5)]
```

**Pitfall:**  
List comprehensions readable honi chahiye. Agar bahut complex logic hai (nested loops with multiple conditions), regular for loop use karo.

**Interview Q:**  
*Q: Django queryset filtering mein list comprehension vs queryset methods kab use karein?*  
A: Queryset methods (filter, exclude) database level pe filtering karte hain (efficient, SQL query mein WHERE clause). List comprehension Python level pe filtering karta hai (inefficient for large data). Hamesha queryset methods prefer karo jab tak in-memory data manipulation na ho.

---

### Stair 1.4: File Handling, Exception Handling

**Explanation:**  
File operations (read/write) aur errors ko gracefully handle karna. Django mein file uploads, logging, aur error handling ke liye critical.

**Why it matters:**  
Production apps mein file uploads (images, documents), error logging, aur robust error handling essential hain.

**Micro-steps:**

1. **Create exception handling examples (error_handling.py):**
```python
import json

# Exception handling basics
def divide_numbers(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print("Error: Cannot divide by zero")
        return None
    except TypeError:
        print("Error: Invalid input types")
        return None
    finally:
        print("Division operation completed")

print(divide_numbers(10, 2))
print(divide_numbers(10, 0))

# File handling (similar to reading uploaded files)
def save_user_data(filename, user_data):
    """Save user data to JSON file"""
    try:
        with open(filename, 'w') as f:
            json.dump(user_data, f, indent=2)
        print(f"Data saved to {filename}")
        return True
    except IOError as e:
        print(f"File error: {e}")
        return False

def load_user_data(filename):
    """Load user data from JSON file"""
    try:
        with open(filename, 'r') as f:
            data = json.load(f)
        return data
    except FileNotFoundError:
        print(f"File {filename} not found")
        return None
    except json.JSONDecodeError:
        print("Invalid JSON format")
        return None

# Test file operations
user = {
    "username": "testuser",
    "email": "test@example.com",
    "preferences": {"theme": "dark", "notifications": True}
}

save_user_data("user_data.json", user)
loaded = load_user_data("user_data.json")
print(f"Loaded data: {loaded}")

# Custom exceptions (useful in Django services)
class InsufficientStockError(Exception):
    """Raised when product stock is insufficient"""
    pass

def purchase_product(stock, quantity):
    if quantity > stock:
        raise InsufficientStockError(f"Only {stock} items available, cannot purchase {quantity}")
    return stock - quantity

try:
    remaining = purchase_product(5, 10)
except InsufficientStockError as e:
    print(f"Purchase failed: {e}")
```

2. **Run:**
```bash
python3 error_handling.py
```

**Expected Output:**
```
Division operation completed
5.0
Error: Cannot divide by zero
Division operation completed
None
Data saved to user_data.json
Loaded data: {'username': 'testuser', 'email': 'test@example.com', 'preferences': {'theme': 'dark', 'notifications': True}}
Purchase failed: Only 5 items available, cannot purchase 10
```

**Pitfall:**  
`finally` block hamesha execute hota hai, chahe exception aaye ya na aaye. File operations mein `with` statement use karo - ye automatically file close karta hai.

**Interview Q:**  
*Q: Django mein exception handling kaise karte hain?*  
A: Django mein exceptions ko views/middleware level pe handle karte hain. Try-except blocks view logic mein, aur custom exception handling middleware se. Django automatically common exceptions (404, 500) handle karta hai with error pages. Production mein Sentry jaise tools se exceptions track karte hain.

---

### Phase 1 Mini Exercise

**Task:** Create a simple product inventory system with classes  
**File:** `exercises/phase1_inventory.py`

**Requirements:**
1. `Product` class with name, price, stock
2. `Inventory` class jo multiple products manage kare
3. Methods: add_product, remove_product, get_total_value, search_by_name
4. Exception handling for invalid operations
5. Save/load inventory to/from JSON file

**Time:** 1-2 hours

---

## Phase 2: Web Fundamentals

### Stair 2.1: Client-Server Architecture & HTTP Basics

**Explanation:**  
Web ek client-server model pe kaam karta hai. Browser (client) server se request bhejta hai, server response deta hai. HTTP (HyperText Transfer Protocol) ye communication protocol hai.

**Why it matters:**  
Backend developer ka main kaam server-side logic likhna hai jo HTTP requests handle kare aur appropriate responses bheje.

**Key Concepts:**
- **Client:** Browser, mobile app, ya koi bhi application jo request bhejta hai
- **Server:** Application jo requests receive karta hai aur responses bhejta hai
- **HTTP Request:** Client se server ko message (URL, method, headers, body)
- **HTTP Response:** Server se client ko message (status code, headers, body)

**HTTP Request Components:**
```
GET /api/products/123 HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: application/json
Authorization: Bearer token123

[Optional Body for POST/PUT]
```

**HTTP Response Components:**
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 85

{"id": 123, "name": "Laptop", "price": 1000}
```

**Micro-steps:**

1. **Install httpie (user-friendly HTTP client):**
```bash
pip3 install httpie
```

2. **Make GET request to a public API:**
```bash
http GET https://jsonplaceholder.typicode.com/posts/1
```

**Expected Output:**
```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident",
    "body": "quia et suscipit..."
}
```

3. **Make POST request:**
```bash
http POST https://jsonplaceholder.typicode.com/posts title="My Post" body="Content here" userId=1
```

**Expected Output:**
```json
HTTP/1.1 201 Created
Content-Type: application/json

{
    "title": "My Post",
    "body": "Content here",
    "userId": 1,
    "id": 101
}
```

4. **Using curl (alternative):**
```bash
curl -X GET https://jsonplaceholder.typicode.com/posts/1
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -H "Content-Type: application/json" \
  -d '{"title":"My Post","body":"Content","userId":1}'
```

**Pitfall:**  
HTTP is stateless - har request independent hai. Session/authentication maintain karne ke liye cookies, tokens, ya session IDs use hoti hain.

**Interview Q:**  
*Q: HTTP stateless kya hai aur Django session kaise maintain karta hai?*  
A: HTTP stateless protocol hai - server previous requests ko remember nahi karta. Django sessions maintain karne ke liye session ID ek cookie mein store karta hai. Har request pe ye cookie read karke user data retrieve karta hai database/cache se. Session middleware ye automatically handle karta hai.

---

### Stair 2.2: HTTP Methods (GET, POST, PUT, DELETE, PATCH)

**Explanation:**  
HTTP methods define karte hain ki request ka purpose kya hai. RESTful APIs mein ye CRUD operations se map hote hain.

**Why it matters:**  
Django views aur DRF endpoints specific HTTP methods ke liye design kiye jaate hain.

**HTTP Methods:**

| Method | Purpose | CRUD | Idempotent | Safe |
|--------|---------|------|------------|------|
| GET | Retrieve data | Read | Yes | Yes |
| POST | Create new resource | Create | No | No |
| PUT | Update/Replace entire resource | Update | Yes | No |
| PATCH | Partially update resource | Update | No | No |
| DELETE | Remove resource | Delete | Yes | No |

**Micro-steps:**

1. **GET - Retrieve data (safe, no side effects):**
```bash
# Get list of posts
http GET https://jsonplaceholder.typicode.com/posts

# Get single post
http GET https://jsonplaceholder.typicode.com/posts/1

# Query parameters
http GET https://jsonplaceholder.typicode.com/posts userId==1
```

**Expected:** 200 OK with data

2. **POST - Create new resource:**
```bash
http POST https://jsonplaceholder.typicode.com/posts \
  title="Learning Django" \
  body="Django is awesome" \
  userId=1
```

**Expected:** 201 Created with new resource data (including ID)

3. **PUT - Full update (replace entire resource):**
```bash
http PUT https://jsonplaceholder.typicode.com/posts/1 \
  id=1 \
  title="Updated Title" \
  body="Updated body" \
  userId=1
```

**Expected:** 200 OK with updated data. Note: PUT replaces entire resource, so all fields must be provided.

4. **PATCH - Partial update (only specified fields):**
```bash
http PATCH https://jsonplaceholder.typicode.com/posts/1 \
  title="Only title changed"
```

**Expected:** 200 OK with updated data. Only title changes, other fields remain.

5. **DELETE - Remove resource:**
```bash
http DELETE https://jsonplaceholder.typicode.com/posts/1
```

**Expected:** 200 OK or 204 No Content

**Pitfall:**  
PUT aur PATCH ko confuse mat karo. PUT entire resource replace karta hai (all fields chahiye), PATCH sirf specified fields update karta hai. Django/DRF mein dono support karte hain.

**Interview Q:**  
*Q: REST API mein POST vs PUT ka difference kya hai?*  
A: POST naya resource create karta hai, server ID generate karta hai (non-idempotent - multiple calls multiple resources create karenge). PUT existing resource ko update/replace karta hai specific ID pe (idempotent - multiple calls same result denge). Example: POST /posts creates new post, PUT /posts/5 updates post 5.

---

### Stair 2.3: HTTP Status Codes

**Explanation:**  
Status codes 3-digit numbers hain jo response ki category define karte hain - success, error, redirect, etc.

**Why it matters:**  
APIs proper status codes return karte hain taaki clients samajh sake ki request successful hui ya fail. Django/DRF mein hum explicitly status codes set karte hain.

**Status Code Categories:**

**1xx - Informational (rare):**
- 100 Continue
- 101 Switching Protocols

**2xx - Success:**
- 200 OK - Request successful (GET, PUT, PATCH)
- 201 Created - Resource successfully created (POST)
- 204 No Content - Successful but no response body (DELETE)

**3xx - Redirection:**
- 301 Moved Permanently
- 302 Found (Temporary redirect)
- 304 Not Modified (Caching)

**4xx - Client Errors:**
- 400 Bad Request - Invalid syntax/data
- 401 Unauthorized - Authentication required
- 403 Forbidden - Authenticated but no permission
- 404 Not Found - Resource doesn't exist
- 405 Method Not Allowed - Wrong HTTP method
- 422 Unprocessable Entity - Validation errors

**5xx - Server Errors:**
- 500 Internal Server Error - Server-side crash
- 502 Bad Gateway - Upstream server issue
- 503 Service Unavailable - Server overloaded/maintenance

**Micro-steps:**

1. **Test different status codes:**
```bash
# 200 OK
http GET https://jsonplaceholder.typicode.com/posts/1

# 201 Created
http POST https://jsonplaceholder.typicode.com/posts title="Test" body="Test" userId=1

# 404 Not Found
http GET https://jsonplaceholder.typicode.com/posts/9999

# 400 Bad Request (if API validates)
http POST https://jsonplaceholder.typicode.com/posts invalidField="value"
```

2. **Check status in response:**
```bash
# Verbose mode (-v) shows full request/response
http -v GET https://jsonplaceholder.typicode.com/posts/1
```

**Pitfall:**  
401 vs 403 confuse hote hain. 401 = "kaun ho tum?" (authentication missing), 403 = "tumhe permission nahi hai" (authenticated but forbidden). Django mein LoginRequired decorator 401/302 deta hai, PermissionDenied 403 deta hai.

**Interview Q:**  
*Q: API delete operation ke liye 200 vs 204 kab use karein?*  
A: 204 No Content best practice hai jab response body empty ho (resource deleted, kuch return nahi karna). 200 OK tab use karo jab deletion confirmation ya deleted resource ka data return karna ho. DRF default mein 204 return karta hai for successful DELETE.

---

### Stair 2.4: REST API Principles & JSON

**Explanation:**  
REST (Representational State Transfer) ek architectural style hai API design ke liye. JSON (JavaScript Object Notation) data interchange format hai - human-readable aur machine-parseable.

**Why it matters:**  
Modern web APIs mostly RESTful hain with JSON payloads. Django REST Framework specifically RESTful APIs banane ke liye designed hai.

**REST Principles:**

1. **Client-Server:** Separation of concerns
2. **Stateless:** Har request mein complete information honi chahiye
3. **Cacheable:** Responses cache ho sakti hain
4. **Uniform Interface:** Consistent URL/method patterns
5. **Layered System:** Architecture layers mein divided
6. **Resource-Based URLs:** `/users/123` not `/getUser?id=123`

**RESTful URL Patterns:**

```
GET    /api/products       - List all products
GET    /api/products/5     - Get product 5
POST   /api/products       - Create new product
PUT    /api/products/5     - Update product 5 (full)
PATCH  /api/products/5     - Update product 5 (partial)
DELETE /api/products/5     - Delete product 5

Nested resources:
GET    /api/products/5/reviews       - Reviews for product 5
POST   /api/products/5/reviews       - Add review to product 5
DELETE /api/products/5/reviews/10    - Delete review 10 of product 5
```

**JSON Basics:**

JSON Python dict ke similar hai:

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "is_active": true,
  "age": 30,
  "hobbies": ["reading", "coding"],
  "address": {
    "city": "Mumbai",
    "country": "India"
  }
}
```

**Micro-steps:**

1. **Create a JSON file (user.json):**
```json
{
  "username": "djangodev",
  "email": "dev@django.com",
  "profile": {
    "bio": "Backend developer",
    "skills": ["Python", "Django", "PostgreSQL"]
  },
  "posts_count": 25
}
```

2. **Parse JSON in Python:**
```python
import json

# Load from file
with open('user.json', 'r') as f:
    user = json.load(f)

print(f"Username: {user['username']}")
print(f"Skills: {', '.join(user['profile']['skills'])}")

# Convert Python dict to JSON string
user['posts_count'] += 1
json_string = json.dumps(user, indent=2)
print(json_string)

# Save to file
with open('user_updated.json', 'w') as f:
    json.dump(user, f, indent=2)
```

3. **Test REST API patterns:**
```bash
# Good RESTful URLs (resource-based)
http GET https://jsonplaceholder.typicode.com/users/1/posts

# Query parameters for filtering/pagination
http GET https://jsonplaceholder.typicode.com/posts userId==1

# Response is JSON
http GET https://jsonplaceholder.typicode.com/posts/1 --json
```

**Pitfall:**  
RESTful URLs nouns use karte hain, verbs nahi. Wrong: `/api/getUsers`, `/api/deleteProduct/5`. Correct: `GET /api/users`, `DELETE /api/products/5`. HTTP method hi verb hai.

**Interview Q:**  
*Q: REST API kya hai aur SOAP se kaise different hai?*  
A: REST lightweight, stateless architecture hai jo HTTP methods use karta hai aur primarily JSON format mein data exchange karta hai. SOAP (Simple Object Access Protocol) XML-based, heavyweight, strictly defined protocol hai. REST flexible, easy to implement, aur modern web apps mein popular hai. Django REST Framework RESTful APIs banane ke liye optimized hai.

---

### Stair 2.5: Request Headers & Authentication Basics

**Explanation:**  
HTTP headers request/response ke saath metadata send karte hain. Authentication headers user identity verify karne ke liye use hote hain.

**Why it matters:**  
APIs authentication/authorization implement karte hain headers ke through. Django/DRF mein multiple authentication methods support hain.

**Common Request Headers:**

```
Content-Type: application/json          # Body ka format
Accept: application/json                # Client kya format chahta hai
Authorization: Bearer <token>           # Authentication token
User-Agent: Mozilla/5.0                 # Client information
Cookie: sessionid=abc123                # Session/state management
```

**Common Response Headers:**

```
Content-Type: application/json
Content-Length: 256
Set-Cookie: sessionid=xyz789
Access-Control-Allow-Origin: *          # CORS
Cache-Control: max-age=3600
```

**Authentication Methods:**

1. **Basic Auth:** Username:password encoded in Base64
2. **Token Auth:** Token in Authorization header
3. **JWT (JSON Web Token):** Self-contained token with claims
4. **Session Auth:** Session ID in cookie
5. **OAuth2:** Token-based authorization (complex)

**Micro-steps:**

1. **Send custom headers:**
```bash
# Custom header
http GET https://jsonplaceholder.typicode.com/posts/1 \
  X-Custom-Header:MyValue

# Accept JSON
http GET https://jsonplaceholder.typicode.com/posts/1 \
  Accept:application/json

# Content-Type for POST
http POST https://jsonplaceholder.typicode.com/posts \
  Content-Type:application/json \
  title="Test" body="Body"
```

2. **Simulated token authentication:**
```bash
# Mock API with token (replace with real API if available)
http GET https://api.example.com/protected \
  Authorization:"Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

3. **Python requests with headers:**
```python
import requests

# GET with headers
headers = {
    'Authorization': 'Bearer mytoken123',
    'Accept': 'application/json'
}
response = requests.get('https://jsonplaceholder.typicode.com/posts/1', headers=headers)
print(f"Status: {response.status_code}")
print(f"Content-Type: {response.headers['Content-Type']}")
print(f"Data: {response.json()}")

# POST with JSON
data = {'title': 'New Post', 'body': 'Content', 'userId': 1}
response = requests.post('https://jsonplaceholder.typicode.com/posts', json=data)
print(f"Created: {response.json()}")
```

**Pitfall:**  
Authorization header format strict hai: `Authorization: Bearer <token>` (space ke baad token). Session cookies automatic send hoti hain browser se, but API clients mein manually include karni padti hain.

**Interview Q:**  
*Q: JWT vs Session authentication - kab kya use karein?*  
A: Session auth server pe session data store karta hai (database/cache), cookie mein sirf session ID hoti hai - best for traditional web apps. JWT self-contained token hai, server pe state store nahi hoti (stateless) - best for mobile apps, SPAs, microservices. JWT scalable hai but revoke karna mushkil hai. Django dono support karta hai.

---

### Phase 2 Mini Exercise

**Task:** Build a simple HTTP tester  
**File:** `exercises/phase2_http_tester.py`

**Requirements:**
1. Function to make GET/POST requests using requests library
2. Parse response status, headers, JSON body
3. Handle errors (timeouts, invalid JSON)
4. Test against jsonplaceholder.typicode.com
5. Print formatted output

**Time:** 1 hour

---

## Phase 3: Django Basics

### Stair 3.1: Django Installation & Project Setup

**Explanation:**  
Django ek high-level Python web framework hai. Project setup ka matlab environment setup, Django install karna, aur initial project structure banana.

**Why it matters:**  
Clean project setup best practices aur proper virtual environment production issues avoid karte hain.

**Micro-steps:**

1. **Create virtual environment:**
```bash
# Create project folder
mkdir my_django_project && cd my_django_project

# Create virtual environment
python3 -m venv .venv

# Activate (Linux/Mac)
source .venv/bin/activate

# Activate (Windows)
# .venv\Scripts\activate

# Verify
which python  # Should show .venv path
```

**Expected Output:**
```
/home/user/my_django_project/.venv/bin/python
```

2. **Install Django:**
```bash
pip install django

# Check version
django-admin --version
```

**Expected Output:**
```
4.2.7  # or similar
```

3. **Create Django project:**
```bash
django-admin startproject mysite .
# The dot (.) creates project in current folder
```

**Expected Output:**
```
my_django_project/
├── .venv/
├── manage.py
└── mysite/
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

**File explanations:**
- **manage.py:** Command-line utility for project management (run server, migrations, etc.)
- **mysite/:** Main project package
- **__init__.py:** Makes directory a Python package
- **settings.py:** Project configuration (database, apps, middleware)
- **urls.py:** URL routing (maps URLs to views)
- **wsgi.py:** WSGI server entry point (production)
- **asgi.py:** ASGI server entry point (async support)

4. **Run development server:**
```bash
python manage.py runserver
```

**Expected Output:**
```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). ...
Run 'python manage.py migrate' to apply them.

December 13, 2024 - 10:30:00
Django version 4.2.7, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

5. **Open browser:**
```
http://127.0.0.1:8000/
```

**Expected:** Django welcome page with rocket ship

**Pitfall:**  
Virtual environment activate karna mat bhoolna! Agar global Python mein Django install kiya to version conflicts aur dependency issues aa sakte hain. Hamesha project-specific venv use karo.

**Interview Q:**  
*Q: manage.py aur django-admin mein kya difference hai?*  
A: django-admin global utility hai jo kahin se bhi chalti hai. manage.py project-specific wrapper hai jo automatically DJANGO_SETTINGS_MODULE set karta hai. Project ke andar hamesha manage.py use karo - ye convenient hai aur project settings automatically load karta hai.

---

### Stair 3.2: Understanding settings.py

**Explanation:**  
settings.py Django project ki configuration file hai - database, apps, middleware, templates, static files sab yahan configure hote hain.

**Why it matters:**  
Production mein settings ko properly configure karna critical hai - security, performance, aur functionality depends on settings.

**Key Settings Explained:**

**File:** `mysite/settings.py` (selected important parts)

```python
# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = 'django-insecure-...'  # NEVER commit to git!

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True  # Production mein False hona chahiye

ALLOWED_HOSTS = []  # Production mein domain names add karo

# Application definition
INSTALLED_APPS = [
    'django.contrib.admin',      # Admin interface
    'django.contrib.auth',       # Authentication
    'django.contrib.contenttypes',  # Content type system
    'django.contrib.sessions',   # Session framework
    'django.contrib.messages',   # Messaging framework
    'django.contrib.staticfiles', # Static files management
    # Your apps will be added here
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'mysite.urls'  # Main URL configuration

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],  # Template directories (add custom templates path here)
        'APP_DIRS': True,  # Look for templates in each app
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

# Database
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# Static files (CSS, JavaScript, Images)
STATIC_URL = 'static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'  # collectstatic saves here
STATICFILES_DIRS = [BASE_DIR / 'static']  # Development static files

# Media files (user uploads)
MEDIA_URL = 'media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

**Micro-steps:**

1. **Create environment-specific settings (best practice):**

**File:** `mysite/settings_local.py` (for development - add to .gitignore)
```python
from .settings import *

DEBUG = True
ALLOWED_HOSTS = ['localhost', '127.0.0.1']

# Development database
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db_dev.sqlite3',
    }
}

# Simple email backend for development
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
```

**File:** `mysite/settings_prod.py` (for production)
```python
from .settings import *
import os

DEBUG = False
ALLOWED_HOSTS = [os.environ.get('DOMAIN', 'example.com')]

SECRET_KEY = os.environ.get('SECRET_KEY')

# PostgreSQL for production
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('DB_NAME'),
        'USER': os.environ.get('DB_USER'),
        'PASSWORD': os.environ.get('DB_PASSWORD'),
        'HOST': os.environ.get('DB_HOST'),
        'PORT': '5432',
    }
}

# Security settings
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
```

2. **Use environment variables (install python-dotenv):**
```bash
pip install python-dotenv
```

**File:** `.env` (add to .gitignore)
```
DEBUG=True
SECRET_KEY=your-secret-key-here
DATABASE_URL=sqlite:///db.sqlite3
```

**File:** `mysite/settings.py` (add at top)
```python
from pathlib import Path
import os
from dotenv import load_dotenv

load_dotenv()

SECRET_KEY = os.getenv('SECRET_KEY', 'fallback-secret-key')
DEBUG = os.getenv('DEBUG', 'False') == 'True'
```

**Pitfall:**  
SECRET_KEY ko git mein NEVER commit karo! Production mein DEBUG = False hona chahiye warna error details publicly visible honge. ALLOWED_HOSTS empty rakhne se production mein site nahi chalegi.

**Interview Q:**  
*Q: Django mein SECRET_KEY ka purpose kya hai?*  
A: SECRET_KEY cryptographic signing ke liye use hoti hai - sessions, cookies, CSRF tokens, password reset tokens sign karta hai. Agar change ho jaye to existing sessions invalidate ho jayenge. Production mein ye environment variable se load karni chahiye, git mein commit nahi karni.

---

### Stair 3.3: Creating Django Apps

**Explanation:**  
Django "project" overall website hai, "app" ek specific functionality module hai (e.g., blog app, user app, payment app). Apps reusable hote hain across projects.

**Why it matters:**  
Modular architecture code organization aur reusability improve karta hai. Large projects multiple apps mein divide hote hain.

**Micro-steps:**

1. **Create an app:**
```bash
python manage.py startapp blog
```

**Expected Output:**
```
mysite/
├── blog/              # New app folder
│   ├── __init__.py
│   ├── admin.py       # Register models for admin
│   ├── apps.py        # App configuration
│   ├── models.py      # Database models
│   ├── tests.py       # Tests
│   ├── views.py       # View functions/classes
│   └── migrations/    # Database migrations
│       └── __init__.py
├── manage.py
└── mysite/
    └── ...
```

**File explanations:**
- **admin.py:** Admin interface configuration
- **apps.py:** App metadata and configuration
- **models.py:** Database models (tables)
- **views.py:** Request handlers (controllers in MVC)
- **migrations/:** Database schema changes history

2. **Register app in settings:**

**File:** `mysite/settings.py`
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',  # Add your app here
]
```

3. **Best practice app configuration:**

**File:** `blog/apps.py`
```python
from django.apps import AppConfig

class BlogConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'blog'
    verbose_name = 'Blog Management'  # Admin mein display name
    
    def ready(self):
        # Import signals here (we'll learn later)
        import blog.signals  # Example
```

**Then use in settings:**
```python
INSTALLED_APPS = [
    # ...
    'blog.apps.BlogConfig',  # More explicit
]
```

4. **App directory structure (extended):**
```
blog/
├── __init__.py
├── admin.py
├── apps.py
├── models.py
├── views.py
├── urls.py           # Create this (app-specific URLs)
├── forms.py          # Create this (forms)
├── serializers.py    # For DRF (later)
├── tests.py
├── migrations/
├── templates/        # Create this folder
│   └── blog/         # Namespace templates
│       ├── post_list.html
│       └── post_detail.html
└── static/           # Create this folder
    └── blog/         # Namespace static files
        ├── css/
        └── js/
```

**Pitfall:**  
App ko INSTALLED_APPS mein add karna mat bhoolna! Agar add nahi karoge to models detect nahi honge aur migrations nahi banenge. App naam unique hona chahiye project mein.

**Interview Q:**  
*Q: Django project vs app mein kya difference hai?*  
A: Project ek website hai with configuration (settings.py, main urls.py). App ek specific feature module hai (blog, shop, users). Ek project mein multiple apps hote hain. Apps independently develop ho sakte hain aur multiple projects mein reuse ho sakte hain. Best practice: specific functionality ko separate app mein rakhna.

---

### Stair 3.4: URLs & Views Basics

**Explanation:**  
URLs define karte hain ki konsa URL path konse view ko call kare. Views request handlers hain jo HTTP response return karte hain.

**Why it matters:**  
URL routing web framework ka core hai. Django ka URL dispatcher powerful aur flexible hai.

**Micro-steps:**

1. **Create a simple view:**

**File:** `blog/views.py`
```python
from django.http import HttpResponse, JsonResponse
from django.shortcuts import render

# Function-based view (FBV) - simplest form
def hello_world(request):
    """Simple text response"""
    return HttpResponse("Hello, Django!")

def home(request):
    """HTML response"""
    html = """
    <html>
        <head><title>My Blog</title></head>
        <body>
            <h1>Welcome to My Blog</h1>
            <p>Django is awesome!</p>
        </body>
    </html>
    """
    return HttpResponse(html)

def api_posts(request):
    """JSON response (API endpoint)"""
    posts = [
        {"id": 1, "title": "First Post", "author": "Alice"},
        {"id": 2, "title": "Second Post", "author": "Bob"},
    ]
    return JsonResponse({"posts": posts})

def post_detail(request, post_id):
    """View with URL parameter"""
    return HttpResponse(f"Post ID: {post_id}")
```

2. **Create app URLs:**

**File:** `blog/urls.py` (create new file)
```python
from django.urls import path
from . import views

# App-specific URL patterns
urlpatterns = [
    path('', views.home, name='blog_home'),
    path('hello/', views.hello_world, name='hello'),
    path('api/posts/', views.api_posts, name='api_posts'),
    path('posts/<int:post_id>/', views.post_detail, name='post_detail'),
]
```

3. **Include app URLs in project:**

**File:** `mysite/urls.py`
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('blog/', include('blog.urls')),  # All blog URLs under /blog/
]
```

**URL patterns now:**
```
http://127.0.0.1:8000/admin/              -> Django admin
http://127.0.0.1:8000/blog/               -> blog.views.home
http://127.0.0.1:8000/blog/hello/         -> blog.views.hello_world
http://127.0.0.1:8000/blog/api/posts/     -> blog.views.api_posts
http://127.0.0.1:8000/blog/posts/5/       -> blog.views.post_detail (post_id=5)
```

4. **Test the views:**
```bash
# Start server
python manage.py runserver

# In another terminal or browser:
curl http://127.0.0.1:8000/blog/
curl http://127.0.0.1:8000/blog/hello/
curl http://127.0.0.1:8000/blog/api/posts/
curl http://127.0.0.1:8000/blog/posts/42/
```

**Expected Outputs:**
```
# /blog/
<html>...</html>

# /blog/hello/
Hello, Django!

# /blog/api/posts/
{"posts": [{"id": 1, "title": "First Post", "author": "Alice"}, ...]}

# /blog/posts/42/
Post ID: 42
```

5. **URL patterns with different types:**

**File:** `blog/urls.py` (extended)
```python
from django.urls import path
from . import views

urlpatterns = [
    # String parameter
    path('author/<str:username>/', views.author_posts, name='author_posts'),
    
    # Slug (letters, numbers, hyphens, underscores)
    path('posts/<slug:slug>/', views.post_by_slug, name='post_slug'),
    
    # UUID
    path('posts/<uuid:uuid>/', views.post_by_uuid, name='post_uuid'),
    
    # Multiple parameters
    path('posts/<int:year>/<int:month>/', views.posts_by_date, name='posts_by_date'),
]
```

**Pitfall:**  
URL patterns order matters! Django first match ko use karta hai. Agar `path('posts/<int:post_id>/')` ke baad `path('posts/latest/')` rakha to "latest" ko integer samajh ke first pattern match ho jayega. Specific patterns pehle rakho, generic patterns baad mein.

**Interview Q:**  
*Q: Django mein URL name parameter ka kya use hai?*  
A: URL name se templates aur views mein reverse URL lookup kar sakte ho using `reverse()` or `{% url %}` tag. Agar URL path change ho to sirf urls.py mein change karna hoga, templates/views mein hardcoded URLs update nahi karne padenge. Example: `reverse('post_detail', args=[5])` gives `/blog/posts/5/`.

---

(Due to length constraints, I'll continue with the remaining stairs in the next section. The full README.md will include all phases through Phase 7, interview questions, and complete project examples.)

### Stair 3.5: Django Models & ORM

**Explanation:**  
Models Django ka database abstraction layer hain - Python classes jo database tables represent karti hain. ORM (Object-Relational Mapping) SQL likhne ki zaroorat nahi, Python code se database operations.

**Why it matters:**  
Models app ka core data structure define karte hain. Django ORM powerful aur database-agnostic hai.

**Micro-steps:**

1. **Create a model:**

**File:** `blog/models.py`
```python
from django.db import models
from django.contrib.auth.models import User
from django.utils import timezone

class Post(models.Model):
    """Blog post model"""
    # Fields
    title = models.CharField(max_length=200)
    slug = models.SlugField(max_length=200, unique=True)
    author = models.ForeignKey(User, on_delete=models.CASCADE, related_name='posts')
    content = models.TextField()
    published_date = models.DateTimeField(default=timezone.now)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_published = models.BooleanField(default=False)
    
    # Meta options
    class Meta:
        ordering = ['-published_date']  # Latest first
        verbose_name = 'Blog Post'
        verbose_name_plural = 'Blog Posts'
        indexes = [
            models.Index(fields=['-published_date']),
        ]
    
    # String representation
    def __str__(self):
        return self.title
    
    # Custom methods
    def get_absolute_url(self):
        from django.urls import reverse
        return reverse('post_detail', args=[self.id])

class Category(models.Model):
    """Category model"""
    name = models.CharField(max_length=100, unique=True)
    slug = models.SlugField(unique=True)
    description = models.TextField(blank=True)
    
    class Meta:
        verbose_name_plural = 'Categories'
    
    def __str__(self):
        return self.name

# Many-to-many relationship
Post.add_to_class('categories', models.ManyToManyField(Category, related_name='posts', blank=True))
```

**Common Field Types:**
- `CharField` - Short text (max_length required)
- `TextField` - Long text
- `IntegerField`, `FloatField`, `DecimalField` - Numbers
- `BooleanField` - True/False
- `DateField`, `DateTimeField` - Dates
- `EmailField`, `URLField` - Validated fields
- `ForeignKey` - One-to-many relationship
- `ManyToManyField` - Many-to-many relationship
- `OneToOneField` - One-to-one relationship

2. **Create migrations:**
```bash
python manage.py makemigrations blog
```

**Expected Output:**
```
Migrations for 'blog':
  blog/migrations/0001_initial.py
    - Create model Category
    - Create model Post
```

3. **View migration file:**

**File:** `blog/migrations/0001_initial.py` (auto-generated)
```python
from django.conf import settings
from django.db import migrations, models
import django.db.models.deletion
import django.utils.timezone

class Migration(migrations.Migration):
    initial = True
    
    dependencies = [
        migrations.swappable_dependency(settings.AUTH_USER_MODEL),
    ]
    
    operations = [
        migrations.CreateModel(
            name='Category',
            fields=[
                ('id', models.BigAutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('name', models.CharField(max_length=100, unique=True)),
                ('slug', models.SlugField(unique=True)),
                ('description', models.TextField(blank=True)),
            ],
        ),
        migrations.CreateModel(
            name='Post',
            fields=[
                ('id', models.BigAutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('title', models.CharField(max_length=200)),
                ('slug', models.SlugField(max_length=200, unique=True)),
                ('content', models.TextField()),
                ('published_date', models.DateTimeField(default=django.utils.timezone.now)),
                ('created_at', models.DateTimeField(auto_now_add=True)),
                ('updated_at', models.DateTimeField(auto_now=True)),
                ('is_published', models.BooleanField(default=False)),
                ('author', models.ForeignKey(on_delete=django.db.models.deletion.CASCADE, related_name='posts', to=settings.AUTH_USER_MODEL)),
                ('categories', models.ManyToManyField(blank=True, related_name='posts', to='blog.category')),
            ],
            options={
                'verbose_name': 'Blog Post',
                'verbose_name_plural': 'Blog Posts',
                'ordering': ['-published_date'],
            },
        ),
    ]
```

4. **Apply migrations:**
```bash
python manage.py migrate
```

**Expected Output:**
```
Operations to perform:
  Apply all migrations: admin, auth, blog, contenttypes, sessions
Running migrations:
  Applying blog.0001_initial... OK
```

5. **Django shell (test ORM):**
```bash
python manage.py shell
```

```python
# Import models
from blog.models import Post, Category
from django.contrib.auth.models import User

# Create user (if doesn't exist)
user = User.objects.create_user('testuser', 'test@example.com', 'password123')

# Create category
cat = Category.objects.create(name='Technology', slug='technology')

# Create post
post = Post.objects.create(
    title='My First Post',
    slug='my-first-post',
    author=user,
    content='This is the content of my first post.',
    is_published=True
)

# Add category
post.categories.add(cat)

# Query posts
all_posts = Post.objects.all()
published = Post.objects.filter(is_published=True)
tech_posts = Post.objects.filter(categories__slug='technology')
user_posts = Post.objects.filter(author__username='testuser')

# Get single post
post = Post.objects.get(id=1)
# or
post = Post.objects.get(slug='my-first-post')

# Update
post.title = 'Updated Title'
post.save()

# Delete
# post.delete()

# Exit shell
exit()
```

**Pitfall:**  
ForeignKey mein `on_delete` parameter required hai (Django 2.0+). Options: CASCADE (delete related), SET_NULL (set null), PROTECT (prevent deletion), SET_DEFAULT. Migrations run karna mat bhoolna after model changes!

**Interview Q:**  
*Q: Django mein select_related vs prefetch_related ka difference?*  
A: select_related ForeignKey/OneToOne relationships ke liye hai, SQL JOIN use karta hai (single query). prefetch_related ManyToMany/reverse ForeignKey ke liye hai, separate queries use karta hai. Example: `Post.objects.select_related('author')` author ko same query mein fetch karega, `Post.objects.prefetch_related('categories')` categories separate query mein fetch karegi but efficiently.

---

