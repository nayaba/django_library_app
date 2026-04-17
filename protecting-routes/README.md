# Protecting Routes

**Learning objective:** By the end of this lesson, students will be able to restrict access to views using login protection.

---

## Why protect routes?

Not all users should access everything.

Examples:

* Only logged-in users can create data
* Guests can only view

---

## Step 1: Protect FBVs

Use the decorator:

```python id="y3k9qx"
from django.contrib.auth.decorators import login_required

@login_required
def book_create(request):
    ...
```

👉 If not logged in → redirect to login page

---

## Step 2: Protect CBVs

Use mixins:

```python id="t6m2rp"
from django.contrib.auth.mixins import LoginRequiredMixin

class BookCreateView(LoginRequiredMixin, CreateView):
    model = Book
    form_class = BookForm
```

---

## Step 3: What happens automatically?

From your settings:

```python id="4p8kzv"
LOGIN_URL = "login"
```

👉 Django redirects to:

```text id="7k3xjd"
/auth/login/
```

---

## Step 4: Improve user experience

Add message in template:

```html id="q2m8ra"
{% if not user.is_authenticated %}
  <p>Please log in to create a book.</p>
{% endif %}
```

---

## Step 5: Protect multiple views

Good candidates:

* create
* update
* delete

👉 Keep list/detail public if needed

---

## Real-world example

Company system:

* Employee must log in
* Only authorized users can make changes

---

## ⚠️ Common issue (from your project)

You already used:

```python id="z5k3yw"
LoginRequiredMixin
```

👉 Good — but make sure it is added to ALL protected views

---

## 🎓 You Do

1. Add `login_required` to FBV `book_create`

2. Add `LoginRequiredMixin` to:

   * BookUpdateView
   * BookDeleteView

3. Test:

   * logged out → redirect
   * logged in → access

---

## 🧠 Good habits

* Protect write actions (create/update/delete)
* Keep read actions flexible
* Always test logged-in and logged-out states

