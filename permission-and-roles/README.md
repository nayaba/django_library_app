# Permissions & Roles

**Learning objective:** By the end of this lesson, students will be able to restrict actions based on user roles using `UserPassesTestMixin`.

---

## Why permissions matter

Login answers:
👉 “Is the user logged in?”

Permissions answer:
👉 “Is this user allowed to do this action?”

---

## Step 1: Use `UserPassesTestMixin`

From your project:

```python id="q7p2xk"
from django.contrib.auth.mixins import UserPassesTestMixin

class BookUpdateView(UserPassesTestMixin, UpdateView):
    model = Book
```

---

## Step 2: Add permission logic

```python id="n4k9zt"
def test_func(self):
    return self.request.user.role == "Admin"
```

👉 Only users with role "Admin" can update

---

## ⚠️ Important issue (from your project)

Current code:

```python id="z8x1mp"
return self.request.user.role == "Admin" or "superuser"
```

👉 This is incorrect — it will always return True ❌

Fix it:

```python id="j2v7lw"
return self.request.user.role == "Admin" or self.request.user.is_superuser
```

---

## Step 3: What if user fails?

Django will:

* block access
* return a 403 error

---

## Step 4: Optional — customize behavior

```python id="g5k3pr"
from django.core.exceptions import PermissionDenied

def test_func(self):
    if not self.request.user.is_superuser:
        raise PermissionDenied
    return True
```

---

## Step 5: Role field (important concept)

From your models (commented):

```python id="t3p8zc"
# class User(AbstractUser):
#     role = models.CharField(max_length=20)
```

👉 If you want roles:

* you must create a **custom user model**

---

## Real-world example

Company system:

* Employee → can view
* Manager → can edit
* Admin → full access

---

## 🎓 You Do

1. Fix the `test_func()` logic
2. Restrict update view to:

   * only superusers
3. Test:

   * normal user → blocked
   * superuser → allowed

---

## 🧠 Good habits

* Always test permission logic carefully
* Avoid hardcoding roles early
* Use built-in fields like `is_superuser` when possible
