# Authentication Basics

**Learning objective:** By the end of this lesson, students will be able to implement login and logout using Django’s built-in authentication system.

---

## What is authentication?

Authentication answers:
👉 “Who is the user?”

Examples:

* employee login
* admin dashboard access

---

## Step 1: Enable auth routes

From your project:

```python
path("auth/", include("django.contrib.auth.urls"))
```

👉 This gives you:

* `/auth/login/`
* `/auth/logout/`

---

## Step 2: Create login template

`templates/registration/login.html`

```html
{% extends "base.html" %}

{% block content %}
<h1>Login</h1>

<form method="post">
  {% csrf_token %}
  {{ form.as_p }}
  <button>Sign In</button>
</form>
{% endblock %}
```

---

## Step 3: Update settings

From your project:

```python
LOGIN_URL = "login"
LOGIN_REDIRECT_URL = "author_list"
LOGOUT_REDIRECT_URL = "login"
```

👉 Controls where users go after login/logout

---

## Step 4: Show user in UI

From your base template:

```html
{% if user.is_authenticated %}
  Welcome, {{ user.username }}
{% endif %}
```

---

## Step 5: Add logout button

```html
<form action="{% url 'logout' %}" method="post">
  {% csrf_token %}
  <button>Logout</button>
</form>
```

👉 Logout must use POST

---

## Real-world example

In a company system:

* user logs in → sees dashboard
* user logs out → returns to login page

---

## ⚠️ Common issues

### Missing templates

Django looks for:

```text
registration/login.html
```

👉 Folder name must match exactly

---

### Hardcoded URLs

Avoid:

```html
/action="/auth/logout/"
```

Use:

```html
{% url 'logout' %}
```

---

## 🎓 You Do

1. Visit `/auth/login/`
2. Log in with your superuser
3. Confirm redirect to author list
4. Add logout button to navbar

---

## 🧠 Good habits

* Always use Django auth (don’t build from scratch)
* Use `{% url %}` instead of hardcoding
* Keep auth templates inside `registration/`
