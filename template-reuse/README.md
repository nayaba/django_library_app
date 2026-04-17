# Template Reuse (base.html)

**Learning objective:** By the end of this lesson, students will be able to use template inheritance to reuse layout across pages.

---

## Why template reuse matters

Without reuse:

* you repeat the same HTML on every page ❌

With reuse:

* one layout, many pages ✅

---

## Step 1: Create a base template

From your project:

```html
<!-- templates/base.html -->
<!doctype html>
<html>
  <body>
    <nav>
      <a href="{% url 'author_list' %}">Authors</a> |
      <a href="{% url 'book_list' %}">All Books</a>
    </nav>

    <hr>

    {% block content %}{% endblock %}
  </body>
</html>
```

---

## Step 2: Extend the base template

```html
{% extends "base.html" %}
```

👉 Add this to every page

---

## Step 3: Use the content block

```html
{% block content %}
<h1>Authors</h1>
{% endblock %}
```

👉 This fills the base layout

---

## Step 4: Add navigation (from your project)

```html
{% if user.is_authenticated %}
  Welcome, {{ user.username }}
{% endif %}
```

👉 Show different UI based on login

---

## Step 5: Reuse across pages

All your templates now share:

* navigation
* layout
* structure

---

## Real-world example

Think of a company dashboard:

* header = same everywhere
* menu = same everywhere
* content = changes per page

---

## ⚠️ Common issues (from your project)

### Hardcoded logout URL

```html
<form action="/auth/logout/" method="post">
```

👉 Better:

```html
<form action="{% url 'logout' %}" method="post">
```

---

### Empty else block

```html
{% else %}
{% endif %}
```

👉 Add login/signup links here

---

## 🎓 You Do

1. Add `{% extends "base.html" %}` to all templates
2. Add a message when user is NOT logged in
3. Add a link to signup page

---

## 🧠 Good habits

* Always use a base template
* Keep layout separate from content
* Avoid repeating HTML
