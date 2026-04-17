# Full CRUD with Function-Based Views<


**Learning objective:** By the end of this lesson, students will be able to implement full CRUD (Create, Read, Update, Delete) using function-based views.

---

## What is CRUD?

CRUD = the 4 main actions in any app:

* **Create** → add data
* **Read** → view data
* **Update** → edit data
* **Delete** → remove data

---

## 1. CREATE

```python id="c1x8zd"
def author_create(request):
    if request.method == "POST":
        form = AuthorForm(request.POST)
        if form.is_valid():
            author = form.save()
            return redirect("author_detail", pk=author.pk)
    else:
        form = AuthorForm()

    return render(request, "authors/author_form.html", {"form": form})
```

---

## 2. READ (List + Detail)

```python id="v2m4kd"
def author_list(request):
    authors = Author.objects.all()
    return render(request, "authors/author_list.html", {"authors": authors})
```

```python id="z9n1qf"
def author_detail(request, pk):
    author = Author.objects.get(pk=pk)
    return render(request, "authors/author_detail.html", {"author": author})
```

---

## 3. UPDATE

```python id="b7t3xa"
def author_update(request, pk):
    author = Author.objects.get(pk=pk)

    if request.method == "POST":
        form = AuthorForm(request.POST, instance=author)
        if form.is_valid():
            form.save()
            return redirect("author_detail", pk=author.pk)
    else:
        form = AuthorForm(instance=author)

    return render(request, "authors/author_form.html", {"form": form})
```

👉 `instance=author` loads existing data

---

## 4. DELETE

```python id="h4k8mz"
def author_delete(request, pk):
    author = Author.objects.get(pk=pk)

    if request.method == "POST":
        author.delete()
        return redirect("author_list")

    return render(request, "authors/author_confirm_delete.html", {"author": author})
```

👉 Delete should use **POST**, not GET

---

## Step 5: Add URLs

```python id="q6p2vn"
path("authors/", views.author_list, name="author_list"),
path("authors/new/", views.author_create, name="author_create"),
path("authors/<int:pk>/", views.author_detail, name="author_detail"),
path("authors/<int:pk>/edit/", views.author_update, name="author_update"),
path("authors/<int:pk>/delete/", views.author_delete, name="author_delete"),
```

---

## Step 6: Reuse templates

You used one form template:

```html id="t5n3qx"
{{ form.instance.pk|yesno:"Update,Create" }}
```

👉 Same page for create + update

---

## Real-world example

Think of a company dashboard:

* Create → add employee
* Read → view employee list
* Update → edit details
* Delete → remove employee

---

## 🎓 You Do

1. Add update + delete buttons to author detail page
2. Create a delete confirmation page
3. Repeat CRUD for **Book** model

---

## 🧠 Good habits

* Always use POST for delete
* Reuse templates when possible
* Keep naming consistent (`_create`, `_update`)
