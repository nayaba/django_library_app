# Intro to Class-Based Views

**Learning objective:** By the end of this lesson, students will be able to use class-based views (CBVs) to replace function-based views.

---

## What are Class-Based Views?

A **Class-Based View (CBV)** is a class that handles requests.

👉 Instead of writing functions, you use built-in Django classes.

---

## Why use CBVs?

Compare:

### Function-Based View

```python
def author_list(request):
    authors = Author.objects.all()
    return render(request, "authors/author_list.html", {"authors": authors})
```

### Class-Based View

```python
from django.views.generic import ListView

class AuthorListView(ListView):
    model = Author
    template_name = "authors/author_list.html"
```

👉 Much shorter and cleaner

---

## Step 1: Import CBVs

```python
from django.views.generic import ListView, DetailView
```

---

## Step 2: Create a ListView

```python
class AuthorListView(ListView):
    model = Author
    template_name = "authors/author_list.html"
    context_object_name = "authors"
```

---

## Step 3: Create a DetailView

```python
class AuthorDetailView(DetailView):
    model = Author
    template_name = "authors/author_detail.html"
    context_object_name = "author"
```

---

## Step 4: Update URLs

```python
path("authors/", views.AuthorListView.as_view(), name="author_list"),
```

👉 `.as_view()` converts the class into a view

---

## Step 5: Understand what Django does for you

CBVs automatically:

* get data from database
* send it to template
* handle errors

---

## Real-world example

Think of a company tool:

* FBV → manual process
* CBV → automated system

👉 CBVs reduce repeated work

---

## ⚠️ Important note (from your project)

Your current code:

```python
def get_context_data(self, **kwargs):
    ctx = super().get_context_data(**kwargs)
    return
```

👉 This should return `ctx`:

```python
return ctx
```

---

## 🎓 You Do

1. Replace `author_list` FBV with `AuthorListView`
2. Replace `author_detail` FBV with `AuthorDetailView`
3. Test both routes

---

## 🧠 Good habits

* Start with FBVs to understand logic
* Use CBVs to reduce repetition
* Always use `.as_view()` in URLs
