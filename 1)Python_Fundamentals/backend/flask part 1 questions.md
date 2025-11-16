# Flask Interview Q&A — README

> Carefully prepared Q&A covering **every topic and sub-topic** you provided. Each section has interviewer-style questions and concise, improved answers with examples and best practices. Use this as a ready-to-read interview cheat-sheet or README.

---

# 1. Overview: What is Flask?

**Q:** What is Flask and why is it called a *micro-framework*?
**A:** Flask is a lightweight Python web framework. It's called a *micro*-framework because it provides the core building blocks (routing, request handling, templating integration) but intentionally omits many higher-level components (ORM, form library, admin, etc.). This minimalism makes Flask:

* Simple and fast to learn.
* Highly flexible — you pick the tools and extensions you need.
* Ideal for REST APIs, microservices, rapid prototypes, and small-to-medium apps.

**Key features:** built-in development server (Werkzeug), routing, Jinja2 templating, secure cookies (signed sessions), WSGI compliance, easy extension system.

**Analogy:**
Django = full kitchen with everything.
Flask = basic stove; bring the utensils you need.

---

# 2. When to use / not use Flask

**Q:** When should you choose Flask over Django? When not?
**A:** Use Flask when:

* Building REST APIs or microservices.
* You want maximum control over components.
* The project is small-to-medium or a prototype.
* You prefer a gentle learning curve.

Avoid Flask (prefer Django) when:

* Building very large enterprise apps with many built-in needs.
* You need an out-of-the-box admin panel, authentication, or heavy CMS features.
* You want tightly integrated, opinionated "batteries-included" conventions.

---

# 3. Debug Mode & Why `debug=True` only for development

**Q:** What happens when `debug=True`? Why not use it in production?
**A:** `debug=True` enables:

* Detailed error pages and stack traces.
* Interactive debugger in the browser (can execute code).
* Auto-reloader that restarts server when Python files change.

**Security & stability risks:**

1. Interactive debugger can allow arbitrary code execution — **dangerous** if accessible publicly.
2. Stack traces expose internal code and secrets.
3. Auto-reloader adds overhead and should not be relied on in production.

**Best practice:** Use `debug=True` only in development. In production, use `debug=False`, production WSGI servers (Gunicorn / uWSGI), and proper logging.

---

# 4. How Auto-Reload Works

**Q:** How does Flask auto-reload detect changes?
**A:** Flask (Werkzeug) watches the filesystem for changes in Python (`.py`) files. When a change is detected, it restarts the process so the updated code is used. Note:

* Auto-reload watches Python files; changes to templates (`.html`) or static files (`.css/.js`) typically don't trigger a restart — browser refresh is enough.
* In multi-process production servers, rely on deployment tools (systemd, container restart, CI/CD) instead of auto-reload.

---

# 5. `if __name__ == '__main__'` pattern

**Q:** What does `if __name__ == '__main__':` do and why use it?
**A:** Checks if the script is executed directly. If so, `__name__ == '__main__'` is true and you can run `app.run()` or script-specific code. When the file is imported as a module, that block won't run. Benefits:

* Prevents running the dev server during imports (e.g., in tests).
* Lets a file act both as reusable module and executable script.

**Example:**

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello'

if __name__ == '__main__':
    app.run(debug=True)
```

---

# 6. WSGI — what it is and how Flask uses it

**Q:** What is WSGI and how does Flask fit in?
**A:** WSGI (Web Server Gateway Interface) is a Python standard interface between web servers and Python web apps. Flask is WSGI-compliant:

* Development: Werkzeug’s built-in WSGI server.
* Production: Pair Flask with WSGI servers like **Gunicorn** or **uWSGI**, often behind a reverse proxy (Nginx).

**Request flow example:**
Browser → Nginx → Gunicorn (WSGI server) → Flask app.

---

# 7. Routing & Dynamic Routes

**Q:** What are static vs dynamic routes? How do you use type converters?
**A:**

* **Static route:** fixed path, e.g. `@app.route('/about')`.
* **Dynamic route:** contains variables: `@app.route('/user/<username>')` — captures `username` and passes to view.

**Type converters:** enforce type and convert in URL:

* `<int:id>` → matches integers and passes `id` as int.
* `<float:price>`, `<path:filepath>`, `<string:name>` (default), `<uuid:uid>`.

**Example:**

```python
@app.route('/post/<int:post_id>')
def post(post_id):
    # post_id is an int
    ...
```

---

# 8. Query Parameters vs URL Parameters vs Request Body

**Q:** Explain `request.args`, `request.form`, and `request.json`.
**A:**

* `request.args` — URL query parameters (`/search?q=flask&page=2`). Access: `request.args.get('q')`.
* `request.form` — form-encoded POST data (`application/x-www-form-urlencoded` or `multipart/form-data`). Access: `request.form.get('username')`.
* `request.json` or `request.get_json()` — JSON body (`Content-Type: application/json`). Access: `request.get_json()`.

**Table summary:**

| Data Source  | Typical Method | Access                  |
| ------------ | -------------- | ----------------------- |
| Query params | GET            | `request.args.get('k')` |
| Form data    | POST (form)    | `request.form.get('k')` |
| JSON body    | POST/PUT (API) | `request.get_json()`    |

**Extra:** use `request.files` for file uploads (multipart form).

---

# 9. HTTP Methods & When to use them

**Q:** Explain the common HTTP methods and their intended use.
**A:**

* **GET** — Read data (idempotent). Use for fetch/search.
* **POST** — Create resource or submit data (not idempotent).
* **PUT** — Replace resource (idempotent).
* **PATCH** — Partial update (idempotent per semantics).
* **DELETE** — Delete resource.

**How to allow multiple methods:**

```python
@app.route('/user', methods=['GET', 'POST'])
def user():
    if request.method == 'POST':
        ...
    else:
        ...
```

**Idempotency & safety**: design APIs so clients understand repeat behavior.

---

# 10. `@app.route('/user')` vs `@app.route('/user/')` (Trailing slash)

**Q:** Difference and best practice?
**A:**

* `@app.route('/user')` — route without trailing slash. A request to `/user/` will redirect (301) to `/user` automatically if strict slashes default is used.
* `@app.route('/user/')` — route with trailing slash; a request to `/user` redirects to `/user/`.

**Best practice:** Choose one style for resources. For resource collections, trailing slash (`/users/`) is common; for single resources, no trailing slash (`/users/123`). Use `strict_slashes` if you need custom behavior.

---

# 11. `url_for()` and URL building

**Q:** What is `url_for()` and why use it?
**A:** `url_for('view_func_name', **params)` returns the URL for a view function. Advantages:

* Keeps code DRY — route changes won’t break links.
* Handles URL quoting/escaping automatically.
* Works with blueprints and `static` files: `url_for('static', filename='style.css')`.
* Generates absolute or relative URLs with `_external=True`.

**Example:**

```python
@app.route('/post/<int:id>')
def post(id): ...

url = url_for('post', id=10)  # -> '/post/10'
```

---

# 12. Returning Responses & Status Codes

**Q:** How to return JSON, templates, redirects, and set status codes?
**A:**

* **JSON:** `return jsonify({'key':'value'})` or `return json.dumps(...)` + `Response` with content type.
* **Template:** `return render_template('index.html', var=value)`
* **Redirect:** `return redirect(url_for('index'))`
* **Status code:** `return 'Created', 201` or `return jsonify(...), 201`

**Common status codes:**

* `200 OK`, `201 Created`, `204 No Content`, `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`, `500 Internal Server Error`.

---

# 13. Jinja2 Templates — rendering, inheritance, escaping

**Q:** What is Jinja2? How to pass data? What is template inheritance?
**A:** Jinja2 is Flask's template engine for rendering HTML. It supports variable interpolation, control structures, filters, macros, and template inheritance.

**Pass data:**

```python
return render_template('profile.html', user=user_obj)
```

Inside template: `{{ user.name }}`

**Template inheritance (base.html):**
`base.html`

```html
<!doctype html>
<html>
  <head>
    <title>{% block title %}My Site{% endblock %}</title>
  </head>
  <body>
    {% block content %}{% endblock %}
  </body>
</html>
```

`index.html`

```html
{% extends "base.html" %}
{% block title %}Home{% endblock %}
{% block content %}
  <h1>Welcome</h1>
{% endblock %}
```

**Escaping & security:** Jinja auto-escapes variables to prevent XSS. Use `|safe` only for trusted HTML.

---

# 14. Jinja2 filters and loop variables

**Q:** Examples of useful Jinja2 filters and loop vars.
**A:** Filters: `|lower`, `|upper`, `|safe`, `|join`, `|length`, `|replace`, `|datetime` (custom).
Loop variables inside `{% for ... %}`: `loop.index`, `loop.index0`, `loop.first`, `loop.last`, `loop.length`.

---

# 15. Static files

**Q:** How to serve static files and best practices?
**A:** By default, Flask serves files from the `static/` folder and templates from `templates/`. Use `url_for('static', filename='css/style.css')` to generate correct URLs. Example:

```html
<link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
```

**Notes & best practice:**

* Avoid hardcoding `/static/...`.
* In production, offload static serving to Nginx or a CDN for performance.
* You can change `static_folder` when creating `Flask()` instance: `app = Flask(__name__, static_folder='assets')`.

---

# 16. Forms / `request.form` and GET vs POST differences

**Q:** Differences between GET and POST and how to access form data.
**A:**

* GET: parameters visible in URL, idempotent — use `request.args`.
* POST: data in request body, not idempotent — use `request.form` (for standard forms) or `request.get_json()` for JSON APIs.

**Access patterns:**

```python
username = request.form.get('username')          # safe: returns None if not present
age = request.form.get('age', type=int, default=18)
interests = request.form.getlist('interests')    # multiple values
```

---

# 17. File uploads

**Q:** How to handle file uploads safely?
**A:** Steps:

1. Use `<form enctype="multipart/form-data" method="POST">`.
2. Access uploaded file: `file = request.files['file']`.
3. Use `werkzeug.utils.secure_filename()` to sanitize filename.
4. Validate file extension and type.
5. Enforce `MAX_CONTENT_LENGTH` in app config to limit size.
6. Save to a secure uploads directory (ensure directory exists and proper permissions).
7. Prefer storing files in object storage (S3) for production.

**Example:**

```python
from werkzeug.utils import secure_filename
import os

ALLOWED_EXT = {'png','jpg','pdf'}
app.config['MAX_CONTENT_LENGTH'] = 16 * 1024 * 1024  # 16 MB

def allowed_file(filename):
    return '.' in filename and filename.rsplit('.',1)[1].lower() in ALLOWED_EXT

file = request.files.get('file')
if file and allowed_file(file.filename):
    filename = secure_filename(file.filename)
    file.save(os.path.join(upload_dir, filename))
```

---

# 18. CSRF and Flask-WTF

**Q:** What is CSRF and how does Flask-WTF protect against it?
**A:** CSRF (Cross-Site Request Forgery) tricks authenticated users into submitting unintended requests. Flask-WTF automatically adds a CSRF token to forms and validates it on submission.

**How it works:**

1. Generate token and store in session.
2. Include hidden token field in form.
3. Validate token on POST; reject requests with missing/invalid token.

**Example:**

```python
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired

class MyForm(FlaskForm):
    name = StringField('Name', validators=[DataRequired()])
    submit = SubmitField('Send')
```

**Notes:** Flask-WTF requires `SECRET_KEY` configured.

---

# 19. Flash messages & PRG pattern

**Q:** What are flash messages and why use Post-Redirect-Get (PRG)?
**A:** Flash messages are one-time messages stored in session and displayed on next page load (e.g., "Profile updated"). They are typically used after POST actions.

**PRG pattern:** After processing a POST, redirect to a GET page that displays the flash message. This prevents form re-submission when users refresh.

**Example:**

```python
from flask import flash, redirect, url_for

@app.route('/submit', methods=['POST'])
def submit():
    # process form
    flash('Saved successfully', 'success')
    return redirect(url_for('profile'))
```

Template: iterate `get_flashed_messages(with_categories=True)` and show styled alerts.

---

# 20. Data validation and email validation

**Q:** How to validate user input and email addresses?
**A:** **Best practice:** use Flask-WTF + WTForms validators for forms. For email validation:

* Use `Email()` validator from WTForms (or `EmailField` + validator).
* Optionally use `email-validator` library for stricter RFC compliance.
* For simple checks, a regex can be used (not recommended as sole validation).

**Regex example (simplified):**

```python
import re
def is_valid_email(email):
    pattern = r'^[\w\.-]+@[\w\.-]+\.\w+$'
    return re.match(pattern, email) is not None
```

**Production tip:** Prefer server-side validation + client-side UX validation. Never trust client input.

---

# 21. Security reminders & best practices

**Q:** Security best practices for Flask apps?
**A:**

* Never run with `debug=True` in production.
* Use strong `SECRET_KEY` for sessions and CSRF.
* Sanitize filenames with `secure_filename`.
* Validate and sanitize all user input.
* Use HTTPS and secure cookies (`SESSION_COOKIE_SECURE=True`, `SESSION_COOKIE_HTTPONLY=True`).
* Limit upload size with `MAX_CONTENT_LENGTH`.
* Use ORM / parameterized queries to avoid SQL injection.
* Use Content Security Policy (CSP) headers to reduce XSS risks.
* Offload static files to CDN and use caching wisely.

---

# 22. Deployment notes (brief)

**Q:** How to deploy Flask in production?
**A:** Typical deployment stack:

* Reverse proxy: Nginx — handles TLS, static files, buffering.
* WSGI server: Gunicorn or uWSGI — runs multiple worker processes.
* App server: Flask app behind Gunicorn. Example: `gunicorn -w 4 'myapp:create_app()'`.
* Use process managers (systemd) or container orchestration (Docker + Kubernetes) for reliability.
* Use environment-specific configs and secrets (not checked into VCS).

---

# 23. Extra interview-style questions (short, with answers)

**Q:** How do you return JSON responses in Flask?
**A:** Use `from flask import jsonify` and `return jsonify({'k':'v'})`. `jsonify` sets the `application/json` header automatically.

**Q:** How do you handle multiple HTTP methods in a single route?
**A:** `@app.route('/path', methods=['GET','POST'])` and branch on `request.method`.

**Q:** How to send files (download) to user?
**A:** Use `send_from_directory()` or `send_file()` from Flask.

**Q:** What is `Flask(__name__)` argument used for?
**A:** It helps Flask locate static and template folders relative to the module. It also sets the app's import name for resource resolution.

**Q:** How do you structure a larger Flask app?
**A:** Use the *Application Factory* pattern (`create_app()`), Blueprints for modular routes, config classes (`DevelopmentConfig`, `ProductionConfig`), and separate extensions initialization (db, migrate, login, etc.).

**Q:** How to test Flask apps?
**A:** Use Flask's test client: `app.test_client()` with pytest to make requests and assert responses; configure a test database.

---

# 24. Example mini-project skeleton (interview talking point)

**A:** A typical Flask microservice layout:

```
myapp/
├─ app/
│  ├─ __init__.py       # create_app factory, blueprint registration
│  ├─ models.py         # SQLAlchemy models
│  ├─ views/
│  │   ├─ __init__.py
│  │   ├─ auth.py
│  │   └─ api.py
│  ├─ templates/
│  └─ static/
├─ migrations/
├─ tests/
├─ requirements.txt
├─ config.py
└─ wsgi.py
```

Explain application factory, blueprint usage, and why this is suitable for scaling microservices.

---

# 25. Common pitfalls & interview talking points

* Relying on Flask dev server in production.
* Putting secrets in code (use environment variables).
* Not validating uploads or user input.
* Misusing `|safe` in templates — opens XSS.
* Expecting auto-reload to handle everything in production.
* Not using `url_for` leads to brittle links.

---

# 26. Short checklist to mention in interviews (bullet points)

* Flask is a micro-framework (minimal, extensible).
* Use `Flask-WTF` for forms + CSRF.
* Use `secure_filename`, `MAX_CONTENT_LENGTH` for file uploads.
* Use `url_for` and template inheritance (DRY).
* `debug=True` only in dev; production → Gunicorn + Nginx.
* Validate inputs; use ORM and parameterized queries.
* Jinja2 auto-escaping prevents XSS by default.
* Use PRG pattern after POSTs; use flash messages for feedback.

---

# 27. Ready-to-use code snippets (paste-ready)

**Simple app with dynamic route, template, JSON endpoint:**

```python
from flask import Flask, request, jsonify, render_template, url_for, redirect, flash
from werkzeug.utils import secure_filename
import os

app = Flask(__name__)
app.secret_key = 'change-this-to-a-secure-random-value'
app.config['MAX_CONTENT_LENGTH'] = 16 * 1024 * 1024  # 16 MB

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/user/<int:user_id>')
def user_profile(user_id):
    return f'User {user_id}'

@app.route('/api/data', methods=['POST'])
def api_data():
    data = request.get_json()
    if not data:
        return jsonify({'error': 'invalid json'}), 400
    return jsonify({'received': data}), 201

if __name__ == '__main__':
    app.run(debug=True)
```

---

# 28. Common interview questions you should be ready to answer (one-liners to expand in interview)

1. What is Flask and why micro-framework?
2. Flask vs Django — when to pick which?
3. What is WSGI? How to deploy Flask in production?
4. Explain `if __name__ == '__main__'`.
5. What are dynamic routes and type converters?
6. How does `url_for()` help?
7. Differences: `request.args`, `request.form`, `request.json`.
8. How to handle file uploads securely?
9. What is CSRF and how does Flask-WTF handle it?
10. How does template inheritance work?
11. Why `debug=True` is dangerous in production?
12. How do you return JSON with status codes?
13. How to serve static files?
14. What security settings do you enable for production?
15. How to structure a medium-sized Flask app (blueprints, factory)?

---

# Final notes (how to use this README)

* Use this file as your interview guide. Memorize definitions, common pitfalls, and code snippets.
* When answering, give a short definition + example + best practice.
* Where appropriate, mention production differences (dev vs prod), security, and common gotchas.

Got it — **you want a complete, highly-structured, step-by-step practice workbook** for Flask fundamentals (A → D), where:

✔ Each section (A, B, C, D)
✔ Contains multiple **mini-exercises**
✔ Exercises are **small, progressive, stair-wise**
✔ Focus on **routing, HTTP methods, request handling, url_for, templates, forms, query params, JSON**
✔ Helps you understand **when to use what**
✔ Not answers — but real practice tasks to build logic and confidence

Below is your **complete Flask Practice Workbook (A → D)** in **README format**.

---

# 🧠 Flask Hands-On Practice Workbook

A complete step-by-step exercise set from basics → advanced routing → templates → forms & requests.

---

# **A. Routing & Basic Concepts**

## **A1 — Basic Route Exercises**

1. Create a route `/hello` that returns `"Hello Flask!"`.
2. Create a route `/welcome/<name>` that returns `"Welcome, <name>"`.
3. Create a route `/square/<int:n>` that returns the square of the number.
4. Create a route `/today` that returns current date.
5. Create `/status` route that returns `"Server is running"`.

---

## **A2 — Dynamic Route Exercises**

1. Create `/user/<username>` → return “Profile of username”.
2. Create `/age/<int:age>` → return “You are X years old”.
3. Create `/product/<string:name>/<int:id>` → return both name and ID.
4. Create `/calculate/<float:num>` → return its doubled value.
5. Create `/is_even/<int:n>` → return `"Even"` or `"Odd"`.

---

## **A3 — Multiple Routes for Same Function**

1. Create `/home` and `/` both showing “Homepage”.
2. Create `/contact` and `/reach-us` pointing to same function.
3. Create `/item/<id>` and `/product/<id>` sharing the same logic.

---

## **A4 — HTTP Methods (GET/POST) Basics**

1. Create `/method_check` route and return request.method.
2. Create `/login` →

   * GET → return “Login Form”
   * POST → return “Form Submitted”
3. Create `/math` →

   * GET → show instructions
   * POST → process some numbers

---

## **A5 — Query Parameters Exercises (`request.args`)**

1. Create `/search?query=python` → return the query.
2. Create `/add?x=5&y=6` → return x+y.
3. Create `/greet?name=Tabish` → return “Hello Tabish”.
4. Create `/filter?category=books&page=2`.
5. Create `/sort?order=asc` and return order provided.

---

## **A6 — url_for() Practice**

1. Create a route `/profile/<user>` and generate link to it using url_for().
2. Create homepage that contains links to `/about`, `/contact`.
3. Create `/redirect_home` route that redirects using url_for().
4. Generate URL with dynamic parameter using url_for('user', name='Tabish').
5. Create navigation menu using url_for in HTML.

---

---

# **B. Advanced Routing + Response Types**

## **B1 — Handling Multiple HTTP Methods**

1. Create `/feedback` → supports GET & POST.
2. Create `/update/<int:id>` →

   * GET: show update form
   * POST: show updated result
3. Create `/upload` → only POST allowed.
4. Create `/delete/<id>` → only DELETE allowed.
5. Create `/partial_update/<id>` → only PATCH allowed.

---

## **B2 — Return Different Response Types**

1. Return plain text.
2. Return dictionary as JSON (`jsonify`).
3. Return custom status code 201.
4. Return response with headers.
5. Return redirect response.

---

## **B3 — Error Handling Practice**

1. Create custom 404 page.
2. Create custom 500 page.
3. Raise 400 when query param missing.
4. Raise 403 if unauthorized.
5. Try/except block returning “Something failed”.

---

## **B4 — URL Type Converters**

Create routes using:

1. `<int:id>` → return id * 10
2. `<float:val>` → return val / 2
3. `<path:data>` → return entire path
4. `<string:name>` → uppercase the name
5. Custom converter: allow only “yes/no”

---

---

# **C. Templates (Jinja2)**

## **C1 — render_template() Basics**

1. Render `home.html` with simple message.
2. Pass a variable `name` to the template.
3. Pass a dictionary to Jinja template.
4. Pass a list of items.
5. Render based on dynamic route parameter.

---

## **C2 — Jinja2 Variables + Filters**

1. Display name in uppercase.
2. Format a number to 2 decimals.
3. Display first element of a list.
4. Use `|length` filter.
5. Use `|safe` to render HTML (careful).

---

## **C3 — Loops in Templates**

Given a list:

```python
users = ["Tabish", "Aman", "Sara"]
```

Practice:

1. Show each user using loop.
2. Show index with loop.index.
3. Highlight first item using loop.first.
4. Highlight last item.
5. Display count using loop.length.

---

## **C4 — Template Conditions**

1. If user logged in → show logout
2. If count > 5 → show message
3. If empty list → show “No items”
4. If age >= 18 → show “Adult”
5. Use nested if-else.

---

## **C5 — Template Inheritance**

1. Create base.html with header/footer.
2. Create home.html extending base.
3. Create about.html extending base.
4. Add navigation bar in base using url_for().
5. Add custom CSS/JS through blocks.

---

## **C6 — Static Files Exercise**

1. Link CSS file using url_for.
2. Link image in template.
3. Create JS file & use it.
4. Change static folder name → update usage.
5. Serve static file: `/static/manual.pdf`.

---

---

# **D. Forms, Request Data & Validation**

## **D1 — GET vs POST Exercises**

1. Create `/contact` → GET shows form, POST saves data.
2. Create `/calc` → GET show form, POST compute sum.
3. Create `/feedback` with textarea.
4. Create `/choose` using GET query params.
5. Create `/submit` → POST only.

---

## **D2 — request.form Practice**

1. Submit username + password → print both.
2. Submit number → return double.
3. Submit checkbox list → return selected items.
4. Submit radio button → return selection.
5. Throw error if field missing.

---

## **D3 — request.args Practice**

1. `/search?q=flask`
2. `/page?num=5`
3. `/discount?price=200&off=10`
4. `/login?next=/dashboard`
5. Validate missing parameters.

---

## **D4 — request.json Practice**

1. POST JSON `{ "a": 5, "b": 10 }` → return sum.
2. Validate JSON keys.
3. Return error if not JSON.
4. Accept nested JSON.
5. Accept list + return its length.

---

## **D5 — File Upload Exercises**

1. Upload image → save it.
2. Reject files not ending in `.png`.
3. Use `secure_filename`.
4. Limit max file size.
5. Store uploads in `/uploads` folder.

---

## **D6 — Flash Messages Practice**

1. Flash “Login Successful” after login.
2. Flash error when password wrong.
3. Flash warning when input missing.
4. Show message once (PRG pattern).
5. Categorize messages (success/warning/error).

---

## **D7 — Validation Practice**

1. Validate email manually (regex).
2. Validate phone number.
3. Validate password length.
4. Use WTForms for form validation.
5. Use Email validator inside Flask-WTF.

---

# ✔ Final Result

This is a **complete structured Flask exercise workbook** that covers:

* Routing
* HTTP methods
* Query params
* url_for
* Templates (Jinja2)
* Static files
* Forms
* request.form / request.args / request.json
* File uploads
* Validation
* Flash messages
* Best practices





