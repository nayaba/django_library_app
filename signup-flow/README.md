# Signup Flow

**Learning objective:** By the end of this lesson, students will be able to create a user signup flow using Django’s built-in forms.

---

## Why signup matters

Authentication has two parts:

* Login → existing users
* Signup → new users

---

## Step 1: Create a signup view

From your project:

```python id="3t7kq1"
from django.contrib.auth.models import User
from django.contrib.auth.forms import UserCreationForm
from django.views.generic import CreateView
from django.urls import reverse_lazy

class SignUpView(CreateView):
    model = User
    form_class = UserCreationForm
    success_url = reverse_lazy("login")
    template_name = "registration/sign-up.html"
```

---

## Step 2: Add a URL

```python id="7m2vqx"
path("auth/signup", views.SignUpView.as_view(), name="signup")
```

> 💡 Best practice: add a trailing slash → `"auth/signup/"`

---

## Step 3: Create the template

`templates/registration/sign-up.html`

```html id="4r9kzp"
{% extends "base.html" %}

{% block content %}
<h1>Sign up</h1>

<form method="post">
  {% csrf_token %}
  {{ form.as_p }}
  <button>Sign up</button>
</form>
{% endblock %}
```

---

## Step 4: Understand the form

`UserCreationForm` includes:

* username
* password
* password confirmation

👉 Django handles validation automatically

---

## Step 5: Add link to signup

In `base.html`:

```html id="d1k8mc"
{% if not user.is_authenticated %}
  <a href="{% url 'signup' %}">Sign up</a>
{% endif %}
```

---

## Step 6: Test the flow

1. Go to `/auth/signup/`
2. Create a new user
3. Login using `/auth/login/`

---

## Real-world example

Think of a company portal:

* New employee → creates account
* Then logs in → accesses system

---

## ⚠️ Common issues

### Missing slash

```python id="8x2wpl"
path("auth/signup", ...)
```

👉 Should be:

```python id="2n5jrf"
path("auth/signup/", ...)
```

---

### Template name must match

```text id="9p7qka"
registration/sign-up.html
```

👉 Folder must be `registration`

---

## 🎓 You Do

1. Add signup link to navbar
2. Create a new user
3. Login with that user
4. Confirm redirect works

---

## 🧠 Good habits

* Use Django’s built-in auth forms
* Keep signup simple
* Always test full login/signup flow
