### Stair 3.6: Django Admin Interface

**Explanation:**  
Django admin ek automatic admin interface hai jo models ke liye CRUD operations provide karta hai. Zero extra code se powerful admin panel mil jata hai.

**Why it matters:**  
Content management, data entry, aur debugging ke liye invaluable tool hai. Production mein bhi staff users ke liye useful hai.

**Micro-steps:**

1. **Create superuser:**
```bash
python manage.py createsuperuser
```

**Prompts:**
```
Username: admin
Email address: admin@example.com
Password: ********
Password (again): ********
Superuser created successfully.
```

2. **Register models in admin:**

**File:** `blog/admin.py`
```python
from django.contrib import admin
from .models import Post, Category

# Simple registration
# admin.site.register(Post)
# admin.site.register(Category)

# Customized admin (better)
@admin.register(Category)
class CategoryAdmin(admin.ModelAdmin):
    list_display = ['name', 'slug']
    prepopulated_fields = {'slug': ('name',)}
    search_fields = ['name']

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'published_date', 'is_published']
    list_filter = ['is_published', 'published_date', 'categories']
    search_fields = ['title', 'content']
    prepopulated_fields = {'slug': ('title',)}
    date_hierarchy = 'published_date'
    ordering = ['-published_date']
    filter_horizontal = ['categories']  # Better UI for ManyToMany
    
    # Customize form layout
    fieldsets = (
        ('Basic Information', {
            'fields': ('title', 'slug', 'author')
        }),
        ('Content', {
            'fields': ('content', 'categories')
        }),
        ('Publication', {
            'fields': ('is_published', 'published_date')
        }),
    )
    
    # Read-only fields
    readonly_fields = ['created_at', 'updated_at']
    
    # Custom action
    actions = ['make_published']
    
    def make_published(self, request, queryset):
        queryset.update(is_published=True)
    make_published.short_description = "Mark selected posts as published"
```

3. **Access admin:**
```bash
# Start server
python manage.py runserver

# Open browser:
# http://127.0.0.1:8000/admin/
# Login with superuser credentials
```

**Expected:** Admin dashboard with Blog Posts and Categories sections

4. **Advanced admin customization:**

**File:** `blog/admin.py` (extended)
```python
from django.contrib import admin
from django.utils.html import format_html
from .models import Post, Category

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'published_date', 'is_published', 'category_count', 'colored_status']
    
    # Custom column - count categories
    def category_count(self, obj):
        return obj.categories.count()
    category_count.short_description = 'Categories'
    
    # Custom column with HTML
    def colored_status(self, obj):
        if obj.is_published:
            color = 'green'
            text = 'Published'
        else:
            color = 'red'
            text = 'Draft'
        return format_html(
            '<span style="color: {};">{}</span>',
            color, text
        )
    colored_status.short_description = 'Status'
    
    # Inline editing (if you had comments model)
    # inlines = [CommentInline]
```

**Pitfall:**  
Admin mein fields jo editable nahi hain (auto_now, auto_now_add) wo by default show nahi hote. Unhe dekhne ke liye `readonly_fields` mein add karo. Admin URL `/admin/` trailing slash important hai.

**Interview Q:**  
*Q: Django admin ko production mein use karna safe hai?*  
A: Ha, Django admin production-ready hai agar properly secured ho. Best practices: strong passwords, SSL/HTTPS mandatory, custom admin URL (change from /admin/), limit admin access by IP, enable two-factor auth, regular security updates. Many production sites Django admin use karte hain for internal teams.

---

### Stair 3.7: Templates & Template Language

**Explanation:**  
Templates HTML files hain jinmein Django Template Language (DTL) use karke dynamic content inject karte hain. Views context data templates ko pass karte hain.

**Why it matters:**  
Server-side rendering ke liye templates essential hain. Django template system powerful aur secure hai (auto-escapes HTML).

**Micro-steps:**

1. **Create templates directory structure:**
```bash
mkdir -p blog/templates/blog
```

2. **Create base template:**

**File:** `blog/templates/blog/base.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}My Blog{% endblock %}</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        header {
            background-color: #333;
            color: white;
            padding: 20px;
            margin-bottom: 20px;
        }
        nav a {
            color: white;
            margin-right: 15px;
            text-decoration: none;
        }
        .content {
            background-color: white;
            padding: 20px;
            border-radius: 5px;
        }
        footer {
            margin-top: 20px;
            text-align: center;
            color: #666;
        }
    </style>
    {% block extra_css %}{% endblock %}
</head>
<body>
    <header>
        <h1>My Django Blog</h1>
        <nav>
            <a href="{% url 'blog_home' %}">Home</a>
            <a href="{% url 'post_list' %}">All Posts</a>
            <a href="{% url 'admin:index' %}">Admin</a>
        </nav>
    </header>
    
    <div class="content">
        {% block content %}
        {% endblock %}
    </div>
    
    <footer>
        <p>&copy; 2024 My Blog. Built with Django.</p>
    </footer>
    
    {% block extra_js %}{% endblock %}
</body>
</html>
```

3. **Create post list template:**

**File:** `blog/templates/blog/post_list.html`
```html
{% extends 'blog/base.html' %}

{% block title %}All Posts - My Blog{% endblock %}

{% block content %}
<h2>All Blog Posts</h2>

{% if posts %}
    <p>Total posts: {{ posts|length }}</p>
    
    {% for post in posts %}
    <article style="margin-bottom: 30px; padding-bottom: 20px; border-bottom: 1px solid #ddd;">
        <h3>
            <a href="{% url 'post_detail' post.id %}">{{ post.title }}</a>
        </h3>
        <p style="color: #666; font-size: 14px;">
            By {{ post.author.username }} | 
            {{ post.published_date|date:"F d, Y" }} |
            {% if post.is_published %}
                <span style="color: green;">Published</span>
            {% else %}
                <span style="color: red;">Draft</span>
            {% endif %}
        </p>
        <p>{{ post.content|truncatewords:30 }}</p>
        
        {% if post.categories.all %}
        <p><strong>Categories:</strong>
            {% for category in post.categories.all %}
                <span style="background-color: #e0e0e0; padding: 3px 8px; border-radius: 3px; margin-right: 5px;">
                    {{ category.name }}
                </span>
            {% endfor %}
        </p>
        {% endif %}
        
        <a href="{% url 'post_detail' post.id %}">Read more &rarr;</a>
    </article>
    {% endfor %}
    
{% else %}
    <p>No posts available yet.</p>
{% endif %}

{% endblock %}
```

4. **Create post detail template:**

**File:** `blog/templates/blog/post_detail.html`
```html
{% extends 'blog/base.html' %}

{% block title %}{{ post.title }} - My Blog{% endblock %}

{% block content %}
<article>
    <h2>{{ post.title }}</h2>
    
    <p style="color: #666; font-size: 14px;">
        By <strong>{{ post.author.username }}</strong> | 
        Published on {{ post.published_date|date:"F d, Y" }}
    </p>
    
    {% if post.categories.all %}
    <p><strong>Categories:</strong>
        {% for category in post.categories.all %}
            <span style="background-color: #e0e0e0; padding: 3px 8px; border-radius: 3px;">
                {{ category.name }}
            </span>
        {% endfor %}
    </p>
    {% endif %}
    
    <div style="line-height: 1.6; margin-top: 20px;">
        {{ post.content|linebreaks }}
    </div>
    
    <hr style="margin: 30px 0;">
    
    <p>
        <a href="{% url 'post_list' %}">&larr; Back to all posts</a>
    </p>
</article>
{% endblock %}
```

5. **Update views to use templates:**

**File:** `blog/views.py`
```python
from django.shortcuts import render, get_object_or_404
from .models import Post

def post_list(request):
    """Display all posts"""
    posts = Post.objects.filter(is_published=True).select_related('author')
    context = {
        'posts': posts
    }
    return render(request, 'blog/post_list.html', context)

def post_detail(request, post_id):
    """Display single post"""
    post = get_object_or_404(Post, id=post_id, is_published=True)
    context = {
        'post': post
    }
    return render(request, 'blog/post_detail.html', context)
```

6. **Update URLs:**

**File:** `blog/urls.py`
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='blog_home'),
    path('posts/', views.post_list, name='post_list'),
    path('posts/<int:post_id>/', views.post_detail, name='post_detail'),
]
```

7. **Test templates:**
```bash
python manage.py runserver
# Visit: http://127.0.0.1:8000/blog/
```

**Common Template Tags & Filters:**

```django
{# Comments #}

{# Variables #}
{{ variable }}
{{ user.username }}
{{ post.title|upper }}

{# Filters #}
{{ text|lower }}
{{ text|truncatewords:30 }}
{{ date|date:"Y-m-d" }}
{{ value|default:"N/A" }}

{# Tags #}
{% if condition %}...{% endif %}
{% for item in list %}...{% endfor %}
{% url 'view_name' arg1 arg2 %}
{% static 'css/style.css' %}
{% csrf_token %}

{# Template inheritance #}
{% extends 'base.html' %}
{% block content %}...{% endblock %}

{# Include other templates #}
{% include 'partials/header.html' %}
```

**Pitfall:**  
Template inheritance ke liye `{% extends %}` tag file ka first tag hona chahiye (comments ke baad). `{% url %}` tag mein view name quotes mein hona chahiye. Auto-escaping on hai by default, agar HTML render karna hai to `{{ content|safe }}` use karo (carefully!).

**Interview Q:**  
*Q: Django templates vs Jinja2 templates mein kya difference hai?*  
A: Django templates simpler aur secure hain (less powerful Python expressions). Jinja2 more flexible hai (Python expressions allowed in templates). Django default mein auto-escaping on hai (XSS protection). Jinja2 faster hai but Django templates Django ke saath better integrated hain. Django 1.8+ mein Jinja2 bhi support hai as alternative backend.

---

### Stair 3.8: Static Files & Media Files

**Explanation:**  
Static files (CSS, JS, images) development assets hain. Media files user-uploaded content hain. Django dono ko alag handle karta hai.

**Why it matters:**  
Production mein static files efficiently serve karni hoti hain (CDN, caching). User uploads securely handle karni hoti hain.

**Micro-steps:**

1. **Configure static files:**

**File:** `mysite/settings.py`
```python
import os
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

# Static files (CSS, JavaScript, Images)
STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'  # collectstatic saves here
STATICFILES_DIRS = [
    BASE_DIR / 'static',  # Project-level static files
]

# Media files (User uploads)
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

2. **Create static files structure:**
```bash
mkdir -p static/css static/js static/images
mkdir -p blog/static/blog/css blog/static/blog/js
```

3. **Create CSS file:**

**File:** `static/css/style.css`
```css
/* Global styles */
:root {
    --primary-color: #3498db;
    --secondary-color: #2c3e50;
    --success-color: #27ae60;
    --danger-color: #e74c3c;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    line-height: 1.6;
    color: #333;
}

.btn {
    display: inline-block;
    padding: 10px 20px;
    background-color: var(--primary-color);
    color: white;
    text-decoration: none;
    border-radius: 5px;
    transition: background-color 0.3s;
}

.btn:hover {
    background-color: #2980b9;
}

.alert {
    padding: 15px;
    margin-bottom: 20px;
    border-radius: 4px;
}

.alert-success {
    background-color: #d4edda;
    border: 1px solid #c3e6cb;
    color: #155724;
}

.alert-danger {
    background-color: #f8d7da;
    border: 1px solid #f5c6cb;
    color: #721c24;
}
```

4. **Create JavaScript file:**

**File:** `static/js/main.js`
```javascript
// Simple form validation
document.addEventListener('DOMContentLoaded', function() {
    const forms = document.querySelectorAll('form.needs-validation');
    
    forms.forEach(form => {
        form.addEventListener('submit', function(event) {
            if (!form.checkValidity()) {
                event.preventDefault();
                event.stopPropagation();
            }
            form.classList.add('was-validated');
        });
    });
    
    // Auto-dismiss alerts after 5 seconds
    const alerts = document.querySelectorAll('.alert-dismissible');
    alerts.forEach(alert => {
        setTimeout(() => {
            alert.style.display = 'none';
        }, 5000);
    });
});
```

5. **Update base template to use static files:**

**File:** `blog/templates/blog/base.html`
```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}My Blog{% endblock %}</title>
    
    <!-- Static CSS -->
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
    {% block extra_css %}{% endblock %}
</head>
<body>
    <header>
        <img src="{% static 'images/logo.png' %}" alt="Logo" style="height: 40px;">
        <h1>My Django Blog</h1>
        <nav>
            <a href="{% url 'blog_home' %}">Home</a>
            <a href="{% url 'post_list' %}">All Posts</a>
        </nav>
    </header>
    
    <div class="content">
        {% block content %}{% endblock %}
    </div>
    
    <footer>
        <p>&copy; 2024 My Blog</p>
    </footer>
    
    <!-- Static JS -->
    <script src="{% static 'js/main.js' %}"></script>
    {% block extra_js %}{% endblock %}
</body>
</html>
```

6. **Configure URLs for media files (development only):**

**File:** `mysite/urls.py`
```python
from django.contrib import admin
from django.urls import path, include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('blog/', include('blog.urls')),
]

# Serve media files in development
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

7. **Add image field to model:**

**File:** `blog/models.py` (add to Post model)
```python
class Post(models.Model):
    # ... existing fields ...
    featured_image = models.ImageField(upload_to='posts/%Y/%m/', blank=True, null=True)
    
    # ... rest of model ...
```

Install Pillow for image handling:
```bash
pip install Pillow
python manage.py makemigrations
python manage.py migrate
```

8. **Display uploaded image in template:**

**File:** `blog/templates/blog/post_detail.html`
```html
{% if post.featured_image %}
<img src="{{ post.featured_image.url }}" alt="{{ post.title }}" style="max-width: 100%; height: auto;">
{% endif %}
```

9. **Collect static files (for production):**
```bash
python manage.py collectstatic
```

**Expected Output:**
```
You have requested to collect static files at the destination location...
This will overwrite existing files!
Are you sure you want to do this?

Type 'yes' to continue, or 'no' to cancel: yes
120 static files copied to '/path/to/staticfiles'.
```

**Pitfall:**  
`{% load static %}` har template mein jahan static files use ho, load karna hoga (inheritance se automatically nahi milta). Production mein static files serve karne ke liye WhiteNoise ya nginx/Apache use karte hain, Django dev server production ke liye nahi hai.

**Interview Q:**  
*Q: STATIC_ROOT vs STATICFILES_DIRS mein kya difference hai?*  
A: STATICFILES_DIRS development mein static files ke locations hain (project-level static folders). STATIC_ROOT ek single directory hai jahan `collectstatic` command sab static files collect karke copy karti hai for production deployment. Production mein webserver (nginx) STATIC_ROOT se files serve karta hai.

---

(Continuing with more stairs...due to length, I'll create the complete projects now and additional sections)
