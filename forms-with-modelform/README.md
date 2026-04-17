# Forms with ModelForm

**Learning objective:** By the end of this lesson, students will be able to create and use Django `ModelForm` to handle user input.

---

## What is a ModelForm?

A **ModelForm** creates a form from a model.

👉 It automatically:

* builds inputs
* validates data
* saves to database

---

## Step 1: Create a form

Open `main_app/forms.py`:

```python id="8d4k2p"
from django import forms
from .models import Author

class AuthorForm(forms.ModelForm):
    class Meta:
        model = Author
        fields = ["first_name", "last_name", "is_best_seller"]
```

---

## Step 2: Understand the code

* `model` → which model to use
* `fields` → what users can edit

---

## Step 3: Use form in a view

```python id="k2v9xz"
def author_create(request):
    form = AuthorForm()
    return render(request, "authors/author_form.html", {"form": form})
```

---

## Step 4: Display form in template

```html id="7m3cwp"
<form method="post">
  {% csrf_token %}
  {{ form.as_p }}
  <button>Create</button>
</form>
```

👉 `form.as_p` renders inputs automatically

---

## Step 5: ForeignKey in forms

From your project:

```python id="w6t1as"
class BookForm(forms.ModelForm):
```

👉 The `author` field becomes a **dropdown**

---

## Real-world example

Think of a company system:

* Form = employee fills out a request
* Model = stored in database

---

## 🎓 You Do

1. Create a `BookForm`

2. Include:

   * title
   * published_year
   * author

3. Render it in a template

---

## 🧠 Good habits

* Use ModelForms for simple CRUD
* Limit fields (don’t expose everything)
* Always include `{% csrf_token %}`
