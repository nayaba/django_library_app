# Rendering Templates

**Learning objective:** By the end of this lesson, students will be able to pass data from a view to an HTML template and display it.

---

## How data reaches the page

Flow:

1. View gets data
2. View sends data to template
3. Template displays it

---

## Step 1: Pass data from the view

```python
def author_list(request):
    authors = Author.objects.all()
    return render(request, "authors/author_list.html", {"authors": authors})
```

👉 `"authors"` is the name used in the template

---

## Step 2: Display data in the template

Open `templates/authors/author_list.html`:

```html
{% for a in authors %}
  <p>{{ a.first_name }} {{ a.last_name }}</p>
{% endfor %}
```

---

## Step 3: Understand template syntax

* `{{ }}` → display data
* `{% %}` → logic (loops, if statements)

---

## Step 4: Display a single object

```python
def author_detail(request, pk):
    author = Author.objects.get(pk=pk)
    return render(request, "authors/author_detail.html", {"author": author})
```

Template:

```html
<h1>{{ author.first_name }} {{ author.last_name }}</h1>
```

---

## Step 5: Link pages together

```html
<a href="{% url 'author_detail' a.pk %}">
  {{ a.first_name }}
</a>
```

👉 This creates clickable links

---

## Real-world example

* View = manager preparing data
* Template = presentation slide
* User = audience

---

## 🎓 You Do

1. Update your book list template:

```html
{% for book in books %}
  <p>{{ book.title }}</p>
{% endfor %}
```

2. Add a link to book detail page

---

## 🧠 Good habits

* Keep logic in views, not templates
* Use clear variable names (`authors`, `book`)
* Match names between view and template exactly

