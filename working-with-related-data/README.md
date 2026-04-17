# Working with Related Data


**Learning objective:** By the end of this lesson, students will be able to access and display related data between models.

---

## Why this matters

Most apps have connected data.

In your app:

* One **Author** → many **Books**

---

## Step 1: Use the relationship

From your model:

```python id="4m8k2x"
author = models.ForeignKey(Author, on_delete=models.CASCADE, related_name='books')
```

👉 This allows:

```python id="x3p7r9"
author.books.all()
```

---

## Step 2: Get related data in a view

From your project:

```python id="9d2h7k"
def author_detail(request, pk):
    author = Author.objects.get(pk=pk)
    books = author.books.all()
    return render(request, "authors/author_detail.html", {
        "author": author,
        "books": books
    })
```

---

## Step 3: Display in template

```html id="8t1nq6"
<h2>All Books Written</h2>

{% for book in books %}
  <p>{{ book.title }}</p>
{% empty %}
  <p>No books yet.</p>
{% endfor %}
```

---

## Step 4: Link to related objects

```html id="6g2zq4"
<a href="{% url 'book_detail' book.id %}">
  See Book Details
</a>
```

---

## Step 5: Access parent from child

You can also go the other way:

```html id="y7k3p2"
<p>{{ book.author }}</p>
```

👉 Shows the author of the book

---

## Real-world example

Think of a business system:

* Employee → many tasks
* Task → belongs to one employee

👉 Same pattern

---

## ⚠️ Important issue (from your project)

Your CBV:

```python id="5q8n2d"
def get_context_data(self, **kwargs):
    ctx = super().get_context_data(**kwargs)
    return
```

👉 This does NOT pass books

Fix it:

```python id="z4x1kc"
def get_context_data(self, **kwargs):
    ctx = super().get_context_data(**kwargs)
    ctx["books"] = self.object.books.all()
    return ctx
```

---

## 🎓 You Do

1. Show books on author detail page
2. Add empty message if no books
3. Show author name on book detail page

---

## 🧠 Good habits

* Always use `related_name`
* Handle empty data
* Keep relationships simple

