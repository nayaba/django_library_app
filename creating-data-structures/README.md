# Models: Creating Data Structures

**Learning objective:** By the end of this lesson, students will be able to create Django models and understand how they map to database tables.

---

## What is a Model?

A **model** defines how your data is stored.

Think of it like a spreadsheet:

| first_name | last_name | is_best_seller |
| ---------- | --------- | -------------- |
| Aisha      | Khan      | True           |

👉 Each row = one object
👉 Each column = one field

---

## Step 1: Create your model

Open `main_app/models.py`:

```python
from django.db import models

class Author(models.Model):
    first_name = models.CharField(max_length=80)
    last_name = models.CharField(max_length=80)
    is_best_seller = models.BooleanField(default=False)
```

---

## Step 2: Understand field types

* `CharField` → text
* `BooleanField` → true/false

```python
first_name = models.CharField(max_length=80)
```

👉 `max_length` is required for text fields

---

## Step 3: Add a string display

```python
def __str__(self):
    return f"{self.first_name} {self.last_name}"
```

> 💡 This controls how data appears in the admin panel

---

## Step 4: Create migrations

Run:

```bash
python manage.py makemigrations
```

---

## Step 5: Apply migrations

```bash
python manage.py migrate
```

👉 This creates the database table

---

## Step 6: View in admin

Open `main_app/admin.py`:

```python
from django.contrib import admin
from .models import Author

admin.site.register(Author)
```

Now go to:

```text
http://127.0.0.1:8000/admin/
```

👉 You can add authors!

---

## Real-world example

In a company system:

* Model = database table
* Author = employee
* Fields = employee details

---

## 🎓 You Do

1. Create a new model called `Publisher`
2. Add fields:

   * `name` (text)
   * `location` (text)
3. Run migrations
4. Register it in admin

---

## 🧠 Good habits

* Always run migrations after changing models
* Use clear field names (`first_name`, not `fn`)
* Add `__str__()` early

---

<div style="display: flex; justify-content: space-between;">

  <!-- Previous Lesson -->
  <a href="../creating-data-structures/README.md">⬅ Previous: Creating Data Structures</a>

  <!-- Next Lesson -->
  <a href="../models-relationships/README.md">Next: Models - Relationships ➡</a>

</div>
