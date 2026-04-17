# Intro to Views (Function-Based Views)


**Learning objective:** By the end of this lesson, students will be able to create function-based views (FBVs) to display data.

---

## What is a View?

A **view** controls what happens when a user visits a page.

👉 It:

* gets data from the database
* sends it to a template

---

## Step 1: Create your first view

Open `main_app/views.py`:

```python
from django.shortcuts import render
from .models import Author

def author_list(request):
    authors = Author.objects.all()
    return render(request, "authors/author_list.html", {"authors": authors})
```

---

## Step 2: Understand the code

```python
authors = Author.objects.all()
```

👉 Get all authors from the database

```python
return render(request, "authors/author_list.html", {"authors": authors})
```

👉 Send data to the template

---

## Step 3: Connect the view to a URL

Open `main_app/urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path("authors/", views.author_list, name="author_list"),
]
```

---

## Step 4: Visit the page

Go to:

```text
http://127.0.0.1:8000/authors/
```

👉 Your view is now working 🎉

---

## Step 5: Add a detail view

```python
def author_detail(request, pk):
    author = Author.objects.get(pk=pk)
    return render(request, "authors/author_detail.html", {"author": author})
```

---

## Step 6: Dynamic URLs

```python
path("authors/<int:pk>/", views.author_detail, name="author_detail")
```

👉 `pk` comes from the URL

Example:

```
/authors/1/
```

---

## Real-world example

Think of a business dashboard:

* `/authors/` → list all employees
* `/authors/1/` → view one employee

---

## 🎓 You Do

1. Create a new view:

```python
def book_list(request):
    books = Book.objects.all()
    return render(request, "books/book_list.html", {"books": books})
```

2. Add a URL:

```python
path("books/", views.book_list, name="book_list")
```

3. Visit `/books/`

---

## 🧠 Good habits

* Keep views simple
* Use clear names (`author_list`, not `list1`)
* Always pass data as a dictionary
