# Models: Relationships

**Learning objective:** By the end of this lesson, students will be able to create relationships between models using `ForeignKey`.

---

## Why do we need relationships?

In real systems, data is connected.

Example:

* One **Author** writes many **Books**

| Author | Book   |
| ------ | ------ |
| Aisha  | Book 1 |
| Aisha  | Book 2 |

👉 We should not repeat author data every time
👉 Instead, we **connect** models

---

## Step 1: Create the Book model

Open `models.py`:

```python id="m3b3yq"
class Book(models.Model):
    title = models.CharField(max_length=150)
    published_year = models.PositiveIntegerField(null=True)
    in_print = models.BooleanField(default=True)
```

---

## Step 2: Add a relationship

```python id="c7bqvx"
author = models.ForeignKey(Author, on_delete=models.CASCADE, related_name='books')
```

---

## What this means

* Each **Book** belongs to one **Author**
* One **Author** can have many **Books**

👉 This is called **one-to-many**

---

## Step 3: Understand `on_delete`

```python id="bq8q9j"
on_delete=models.CASCADE
```

👉 If the author is deleted:

* all their books are deleted too

> 💡 Keeps your database clean

---

## Step 4: Understand `related_name`

```python id="czx6qz"
related_name='books'
```

This allows:

```python id="4mj3f0"
author.books.all()
```

👉 Without it, Django would use:

```python id="9c6k9s"
author.book_set.all()
```

---

## Step 5: Add `__str__`

```python id="d9v0c4"
def __str__(self):
    return self.title
```

---

## Step 6: Run migrations

```bash id="n3cskk"
python manage.py makemigrations
python manage.py migrate
```

---

## Step 7: Test in admin

Register your model:

```python id="diyq6p"
admin.site.register(Book)
```

Now you will see:

* a dropdown to select an author when creating a book

---

## Real-world example

Think of a business system:

* Author → employee
* Book → report

👉 One employee creates many reports

---

## 🎓 You Do

1. Add a new field to Book:

```python id="k2y1l0"
price = models.FloatField()
```

2. Run migrations
3. Create 2 authors
4. Add multiple books for one author
5. Test:

```python id="3m1r4g"
author.books.all()
```

---

## 🧠 Good habits

* Always use `related_name` for readability
* Think about relationships before building models
* Use `CASCADE` carefully (it deletes data!)

---

<div style="display: flex; justify-content: space-between;">

  <!-- Previous Lesson -->
  <a href="../models-relationships/README.md">⬅ Previous: Models - Relationships</a>

  <!-- Next Lesson -->
  <a href="../admin-panel/README.md">Next: Admin Panel ➡</a>

</div>
