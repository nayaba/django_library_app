# Debugging Common Issues

**Learning objective:** By the end of this lesson, students will be able to identify and fix common Django errors in views, templates, and URLs.

---

## Why debugging matters

All developers:
👉 make mistakes
👉 fix mistakes

👉 This is a core skill

---

## 1. View not working (wrong return)

From your project:

```python
def get_context_data(self, **kwargs):
    ctx = super().get_context_data(**kwargs)
    return
```

❌ Problem:

* returns nothing

✅ Fix:

```python
return ctx
```

---

## 2. Missing data in template

Problem:

* template expects `books`
* view does not send it

✅ Fix:

```python
ctx["books"] = self.object.books.all()
```

---

## 3. Wrong template logic

From your project:

```html
{% for book in books %}
```

Inside **book_detail.html**

❌ Problem:

* detail page should show ONE book

✅ Fix:

```html
<h1>{{ book.title }}</h1>
```

---

## 4. Duplicate URLs

```python
path("authors/", views.author_list, ...)
path("authors/", views.AuthorListView.as_view(), ...)
```

❌ Problem:

* one overrides the other

✅ Fix:

* keep only one

---

## 5. Wrong URL name

```python
name='book_create'  # used for update
```

❌ Problem:

* confusing naming

✅ Fix:

```python
name='book_update'
```

---

## 6. Template not found

Problem:

* wrong folder name

Example:

```text
template/authors/
```

❌ Should be:

```text
templates/authors/
```

---

## 7. Auth issues

Problem:

* login page not working

Check:

* `registration/login.html` exists
* auth URLs included

---

## 8. Permission logic bug

```python
return self.request.user.role == "Admin" or "superuser"
```

❌ Always true

✅ Fix:

```python
return self.request.user.is_superuser
```

---

## Debugging strategy

Follow this order:

1. Check error message
2. Check view
3. Check URL
4. Check template
5. Print data

Example:

```python
print(authors)
```

---

## Real-world mindset

Debugging is not failure.

👉 It is how developers learn
👉 It is expected in every job

---

## 🎓 You Do

Fix these:

1. Fix `get_context_data()`
2. Fix `book_detail.html`
3. Fix duplicate author route
4. Fix permission logic

---

## 🧠 Good habits

* Read error messages carefully
* Change one thing at a time
* Test often

---

## ✅ Final outcome

You can now:

* Build a full Django app
* Implement CRUD
* Add authentication
* Debug real issues
