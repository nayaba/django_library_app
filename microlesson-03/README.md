
# Admin Panel

**Learning objective:** By the end of this lesson, students will be able to register models and manage data using the Django admin panel.

---

## What is the Admin Panel?

Django gives you a built-in dashboard to manage your data.

👉 No frontend needed
👉 Great for testing and internal tools

---

## Step 1: Create a superuser

Run:

```bash id="7v9l1k"
python manage.py createsuperuser
```

Follow the prompts:

* username
* email (optional)
* password

---

## Step 2: Open the admin panel

Visit:

```text id="k8r2dm"
http://127.0.0.1:8000/admin/
```

Login with your credentials.

---

## Step 3: Register your models

Open `main_app/admin.py`:

```python id="g3j0zq"
from django.contrib import admin
from .models import Author, Book

admin.site.register(Author)
admin.site.register(Book)
```

---

## Step 4: Add data

Now you can:

* create authors
* create books
* link books to authors

👉 The relationship will appear as a dropdown

---

## Step 5: Understand what you see

Each model becomes a section:

* Authors
* Books

Each record:

* shows using `__str__()`

---

## Improve your admin (optional)

You can customize how data appears:

```python id="3x7v8p"
class AuthorAdmin(admin.ModelAdmin):
    list_display = ("first_name", "last_name", "is_best_seller")

admin.site.register(Author, AuthorAdmin)
```

👉 This adds columns to the admin table

---

## Real-world example

In a company:

* Admin panel = internal dashboard
* Used by staff (not customers)
* Quickly manage data without building UI

---

## 🎓 You Do

1. Register `Author` and `Book`
2. Create:

   * 2 authors
   * 3 books
3. Make one author a best seller
4. Verify:

   * books are linked to authors

---

## 🧠 Good habits

* Always use admin to test your models first
* Add `__str__()` for readable data
* Use admin before building frontend pages
