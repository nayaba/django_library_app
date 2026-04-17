# CRUD with Class-Based Views

**Learning objective:** By the end of this lesson, students will be able to implement full CRUD using Django’s built-in class-based views.

---

## Why this matters

With CBVs, Django can handle CRUD for you.

👉 Less code
👉 Faster development
👉 Cleaner structure

---

## Step 1: Import CRUD views

```python id="8wz2mf"
from django.views.generic import CreateView, UpdateView, DeleteView
from django.urls import reverse, reverse_lazy
```

---

## 1. CREATE (CreateView)

```python id="r9q2jd"
class AuthorCreateView(CreateView):
    model = Author
    form_class = AuthorForm
    template_name = "authors/author_form.html"

    def get_success_url(self):
        return reverse("author_detail", kwargs={"pk": self.object.pk})
```

👉 Django:

* shows form
* validates
* saves

---

## 2. UPDATE (UpdateView)

```python id="u4k8xt"
class AuthorUpdateView(UpdateView):
    model = Author
    form_class = AuthorForm
    template_name = "authors/author_form.html"

    def get_success_url(self):
        return reverse("author_detail", kwargs={"pk": self.object.pk})
```

👉 Automatically loads existing data

---

## 3. DELETE (DeleteView)

```python id="m3d7az"
class AuthorDeleteView(DeleteView):
    model = Author
    template_name = "authors/author_confirm_delete.html"
    success_url = reverse_lazy("author_list")
```

👉 Uses confirmation page

---

## Step 2: Add URLs

```python id="v6y1nk"
path("authors/new/", views.AuthorCreateView.as_view(), name="author_create"),
path("authors/<int:pk>/edit/", views.AuthorUpdateView.as_view(), name="author_update"),
path("authors/<int:pk>/delete/", views.AuthorDeleteView.as_view(), name="author_delete"),
```

---

## Step 3: Understand `reverse` vs `reverse_lazy`

* `reverse()` → used inside methods
* `reverse_lazy()` → used at class level

---

## Step 4: Book example (from your project)

```python id="7w2nqe"
class BookCreateView(CreateView):
    model = Book
    form_class = BookForm
```

👉 Same pattern works for all models

---

## ⚠️ Common issue (from your project)

```python id="p8z6rf"
name='book_create'  # used for update
```

👉 Should be:

```python id="n2d4cx"
name='book_update'
```

---

## Real-world example

In a company app:

* Create → add record
* Update → edit record
* Delete → remove record

👉 CBVs standardize all of this

---

## 🎓 You Do

1. Convert Book CRUD to CBVs
2. Add create, update, delete routes
3. Test full flow:

   * create book
   * edit book
   * delete book

---

## 🧠 Good habits

* Reuse templates (`author_form.html`)
* Keep naming consistent
* Use CBVs for standard CRUD
