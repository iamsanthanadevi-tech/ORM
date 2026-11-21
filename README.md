# Ex02 Django ORM Web Application
# Date:21-11-2026
# AIM
To develop a Django application to store and retrieve data from a bank loan database using Object Relational Mapping(ORM).

# DESIGN STEPS
## STEP 1:
Clone the problem from GitHub

## STEP 2:
Create a new app in Django project

## STEP 3:
Enter the code for admin.py and models.py

## STEP 4:
Execute Django admin and create details for 10 cars

# PROGRAM

# FoodieHub – Online Food Delivery Management System

## PROGRAM

### 1. menu/models.py

```python
from django.db import models

class FoodItem(models.Model):
    food_name = models.CharField(max_length=100)
    category = models.CharField(max_length=50)
    price = models.DecimalField(max_digits=8, decimal_places=2)
    restaurant_name = models.CharField(max_length=100)
    description = models.TextField()
    is_available = models.BooleanField(default=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.food_name
```

### 2. menu/views.py

```python
from django.shortcuts import render
from .models import FoodItem

def home(request):
    foods = FoodItem.objects.all()

    return render(request, 'index.html', {
        'foods': foods
    })
```

### 3. menu/urls.py

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

### 4. FoodieHub/urls.py

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('menu.urls')),
]
```

### 5. menu/admin.py

```python
from django.contrib import admin
from .models import FoodItem

admin.site.register(FoodItem)
```

### 6. FoodieHub/settings.py

Add `menu` inside `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'menu',
]
```

### 7. menu/templates/index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>FoodieHub</title>
    <style>
        body {
            font-family: Arial;
            background: #fff8f0;
            margin: 0;
            padding: 20px;
        }

        h1 {
            text-align: center;
            color: #e85d04;
        }

        .food-container {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 20px;
        }

        .food-card {
            background: white;
            padding: 15px;
            border-radius: 12px;
            box-shadow: 0 3px 10px #ccc;
        }

        .price {
            color: #e85d04;
            font-weight: bold;
        }
    </style>
</head>
<body>

<h1>FoodieHub – Delicious Food</h1>

<div class="food-container">
    {% for food in foods %}
    <div class="food-card">
        <h3>{{ food.food_name }}</h3>
        <p>Category: {{ food.category }}</p>
        <p>Restaurant: {{ food.restaurant_name }}</p>
        <p class="price">₹{{ food.price }}</p>
        <p>{{ food.description }}</p>

        {% if food.is_available %}
            <p>Available</p>
        {% else %}
            <p>Currently Unavailable</p>
        {% endif %}
    </div>
    {% empty %}
        <p>No food items available.</p>
    {% endfor %}
</div>

</body>
</html>
```

# OUTPUT
<img width="1917" height="1010" alt="Screenshot 2026-11-21 084644" src="https://github.com/user-attachments/assets/35f4f6fa-7113-4d62-83ed-a23f4fc61b14" />


## RESULT

Thus, the FoodieHub online food delivery application was successfully developed using Django ORM. The FoodItem table was created with multiple fields, and 10 food records were added successfully. The food details were retrieved from the database and displayed on the website in an organized 5 × 2 grid layout.
