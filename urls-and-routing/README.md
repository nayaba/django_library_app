# URLs & Routing

**Learning objective:** By the end of this lesson, students will be able to connect URLs to views and use dynamic routing.

---

## What is routing?

Routing connects a **URL → view**.

Example:

```text
/authors/ → author_list view
```

---

## Step 1: Create a URL pattern

Open `main_app/urls.py`:

```python id="u1w8ra"
from django.urls import path
from . import views

urlpatterns = [
    path("authors/", views.author_list, name="author_list"),
]
```

👉 When user visits `/authors/`, Django runs the view

---

## Step 2: Project-level routing

Open `library_project/urls.py`:

```python id="k4rj6z"
from django.urls import path, include

urlpatterns = [
    path("", include("main_app.urls")),
]
```

👉 This connects your app to the main project

---

## Step 3: Dynamic URLs

```python id="q9t2kc"
path("authors/<int:pk>/", views.author_detail, name="author_detail")
```

👉 `<int:pk>` means:

* Django expects a number
* It passes it to the view

---

## Step 4: Use the value in the view

```python id="v0f8dx"
def author_detail(request, pk):
    author = Author.objects.get(pk=pk)
```

---

## Step 5: Generate URLs in templates

```html id="z6j3np"
<a href="{% url 'author_detail' a.pk %}">
  {{ a.first_name }}
</a>
```

👉 Avoid hardcoding URLs

---

## Step 6: Understand naming

```python id="n7l3kd"
name="author_detail"
```

👉 This lets Django find the route by name

---

## Real-world example

Think of a website:

* `/employees/` → list
* `/employees/5/` → one employee

---

## ⚠️ Common mistakes (from your project)

### Duplicate route

```python id="c5m9xa"
path("authors/", views.author_list, ...)
path("authors/", views.AuthorListView.as_view(), ...)
```

👉 Only one will work (the last one)

---

### Inconsistent parameter names

```python id="r3k2pf"
< int:pk >
< int:book_id >
```

👉 Both work, but be consistent

---

### Incorrect naming

```python id="y7t4lm"
name='book_create'  # used for update
```

👉 Should match the action

---

## 🎓 You Do

1. Add a route for books:

```python id="p4j6zx"
path("books/", views.book_list, name="book_list")
```

2. Add a detail route:

```python id="c8v2mq"
path("books/<int:pk>/", views.book_detail, name="book_detail")
```

3. Link to it in your template

---

## 🧠 Good habits

* Always use `name=` in URLs
* Use `{% url %}` in templates
* Keep naming consistent
