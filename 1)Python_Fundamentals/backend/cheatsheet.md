# Python Backend Developer - Quick Reference Cheatsheet

## Django Commands

### Project & App Management
```bash
# Create project
django-admin startproject myproject

# Create app
python manage.py startapp myapp

# Run development server
python manage.py runserver
python manage.py runserver 0.0.0.0:8000  # Allow external access
python manage.py runserver 3000  # Custom port
```

### Database & Migrations
```bash
# Create migrations
python manage.py makemigrations
python manage.py makemigrations myapp  # Specific app

# Apply migrations
python manage.py migrate
python manage.py migrate myapp  # Specific app
python manage.py migrate myapp 0005  # Specific migration

# Show migrations
python manage.py showmigrations

# Rollback migration
python manage.py migrate myapp 0003  # Rollback to migration 0003

# SQL for migration (without running)
python manage.py sqlmigrate myapp 0001
```

### User Management
```bash
# Create superuser
python manage.py createsuperuser

# Change user password
python manage.py changepassword username
```

### Shell & Testing
```bash
# Django shell
python manage.py shell
python manage.py shell_plus  # If django-extensions installed

# Run tests
python manage.py test
python manage.py test myapp
python manage.py test myapp.tests.test_models

# Coverage
coverage run --source='.' manage.py test
coverage report
coverage html
```

### Static Files
```bash
# Collect static files
python manage.py collectstatic
python manage.py collectstatic --noinput  # No prompts
```

### Database
```bash
# Database shell
python manage.py dbshell

# Flush database (delete all data)
python manage.py flush
```

## HTTP Status Codes

### Success (2xx)
- **200 OK** - Request successful
- **201 Created** - Resource created
- **204 No Content** - Success, no response body

### Client Errors (4xx)
- **400 Bad Request** - Invalid syntax/data
- **401 Unauthorized** - Authentication required
- **403 Forbidden** - No permission
- **404 Not Found** - Resource not found
- **405 Method Not Allowed** - Wrong HTTP method
- **422 Unprocessable Entity** - Validation failed

### Server Errors (5xx)
- **500 Internal Server Error** - Server crash
- **502 Bad Gateway** - Upstream server issue
- **503 Service Unavailable** - Server overload

## Django ORM Quick Reference

### Basic Queries
```python
# Get all
Model.objects.all()

# Filter
Model.objects.filter(field=value)
Model.objects.filter(field__gte=value)  # Greater than or equal
Model.objects.filter(field__contains='text')  # Case-sensitive
Model.objects.filter(field__icontains='text')  # Case-insensitive

# Exclude
Model.objects.exclude(field=value)

# Get single object
Model.objects.get(id=1)
Model.objects.get(field=value)  # Must return exactly one

# Get or 404
from django.shortcuts import get_object_or_404
obj = get_object_or_404(Model, id=1)

# First & Last
Model.objects.first()
Model.objects.last()

# Count
Model.objects.count()
Model.objects.filter(status='active').count()

# Exists
Model.objects.filter(email='test@example.com').exists()

# Order by
Model.objects.order_by('created_at')  # Ascending
Model.objects.order_by('-created_at')  # Descending

# Limit (slicing)
Model.objects.all()[:10]  # First 10
Model.objects.all()[10:20]  # 10-20

# Select related (JOIN for ForeignKey)
Post.objects.select_related('author').all()

# Prefetch related (for ManyToMany)
Post.objects.prefetch_related('categories').all()

# Aggregate
from django.db.models import Count, Sum, Avg
Model.objects.aggregate(Count('id'))
Model.objects.aggregate(total=Sum('price'))

# Annotate
Model.objects.annotate(num_posts=Count('posts'))

# Q objects (complex queries)
from django.db.models import Q
Model.objects.filter(Q(status='active') | Q(is_featured=True))
```

### Create, Update, Delete
```python
# Create (Method 1)
obj = Model(field1='value1', field2='value2')
obj.save()

# Create (Method 2)
obj = Model.objects.create(field1='value1', field2='value2')

# Update single object
obj = Model.objects.get(id=1)
obj.field = 'new_value'
obj.save()

# Bulk update
Model.objects.filter(status='pending').update(status='active')

# Delete single
obj = Model.objects.get(id=1)
obj.delete()

# Bulk delete
Model.objects.filter(status='inactive').delete()

# Get or create
obj, created = Model.objects.get_or_create(
    email='test@example.com',
    defaults={'name': 'Test User'}
)

# Update or create
obj, created = Model.objects.update_or_create(
    email='test@example.com',
    defaults={'name': 'Updated Name'}
)
```

## Django REST Framework

### Serializers
```python
from rest_framework import serializers

# ModelSerializer
class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = ['id', 'title', 'content', 'author']
        read_only_fields = ['id', 'created_at']
        
    def validate_title(self, value):
        if len(value) < 5:
            raise serializers.ValidationError("Title too short")
        return value

# Nested serializer
class PostSerializer(serializers.ModelSerializer):
    author = UserSerializer(read_only=True)
    class Meta:
        model = Post
        fields = ['id', 'title', 'author']
```

### Views
```python
from rest_framework import viewsets, status
from rest_framework.decorators import action
from rest_framework.response import Response

# ViewSet
class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
    permission_classes = [IsAuthenticated]
    
    # Custom action
    @action(detail=True, methods=['post'])
    def publish(self, request, pk=None):
        post = self.get_object()
        post.status = 'published'
        post.save()
        return Response({'status': 'published'})
```

### URLs
```python
from rest_framework.routers import DefaultRouter

router = DefaultRouter()
router.register(r'posts', PostViewSet)

urlpatterns = [
    path('api/', include(router.urls)),
]
```

### Authentication
```python
# Token authentication
from rest_framework.authtoken.models import Token
token = Token.objects.create(user=user)

# JWT (Simple JWT)
from rest_framework_simplejwt.tokens import RefreshToken
refresh = RefreshToken.for_user(user)
access = refresh.access_token
```

## Common Settings

### Database (PostgreSQL)
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydb',
        'USER': 'myuser',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

### Static & Media Files
```python
STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'
STATICFILES_DIRS = [BASE_DIR / 'static']

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

### CORS
```python
INSTALLED_APPS += ['corsheaders']
MIDDLEWARE = ['corsheaders.middleware.CorsMiddleware', ...other middleware]

CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
]
```

## Testing

### Basic Test
```python
from django.test import TestCase
from .models import Post

class PostModelTest(TestCase):
    def setUp(self):
        self.post = Post.objects.create(title='Test')
    
    def test_post_creation(self):
        self.assertEqual(self.post.title, 'Test')
```

### API Test
```python
from rest_framework.test import APITestCase
from rest_framework import status

class PostAPITest(APITestCase):
    def test_create_post(self):
        url = '/api/posts/'
        data = {'title': 'Test', 'content': 'Content'}
        response = self.client.post(url, data)
        self.assertEqual(response.status_code, status.HTTP_201_CREATED)
```

## Docker Commands

```bash
# Build and run
docker-compose up --build

# Run in background
docker-compose up -d

# Stop
docker-compose down

# View logs
docker-compose logs -f web

# Execute command
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser

# Rebuild
docker-compose build --no-cache
```

## Git Commands

```bash
# Initialize
git init
git add .
git commit -m "Initial commit"

# Branches
git branch feature-name
git checkout feature-name
git checkout -b feature-name  # Create and checkout

# Push
git push origin main

# Pull
git pull origin main

# Status
git status
git log --oneline
```

## Environment Variables

### .env file
```
DEBUG=True
SECRET_KEY=your-secret-key
DATABASE_URL=postgresql://user:pass@localhost/dbname
ALLOWED_HOSTS=localhost,127.0.0.1
```

### Load in settings.py
```python
from dotenv import load_dotenv
import os

load_dotenv()

DEBUG = os.getenv('DEBUG', 'False') == 'True'
SECRET_KEY = os.getenv('SECRET_KEY')
```

## Common Patterns

### Custom Manager
```python
class PublishedManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(status='published')

class Post(models.Model):
    objects = models.Manager()
    published = PublishedManager()
```

### Signals
```python
from django.db.models.signals import post_save
from django.dispatch import receiver

@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)
```

### Custom Middleware
```python
class CustomMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
    
    def __call__(self, request):
        # Before view
        response = self.get_response(request)
        # After view
        return response
```

## Deployment Checklist

- [ ] `DEBUG = False`
- [ ] Set `SECRET_KEY` from environment
- [ ] Configure `ALLOWED_HOSTS`
- [ ] Use PostgreSQL (not SQLite)
- [ ] `collectstatic`
- [ ] Configure static file serving
- [ ] Enable HTTPS
- [ ] Set up logging
- [ ] Configure CORS
- [ ] Database backups
- [ ] Monitoring (Sentry)
- [ ] Environment variables
