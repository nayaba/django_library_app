# Handling POST Requests (Form Submission)

**Learning objective:** By the end of this lesson, students will be able to handle form submissions using POST, validate data, and save it to the database.

---

## What is GET vs POST?

* **GET** → show the form
* **POST** → submit the form

👉 Same view handles both

---

## Step 1: Update your view

```python id="t2x9kp"
def author_create(request):
    if request.method == "POST":
        form = AuthorForm(request.POST)
        if form.is_valid():
            author = form.save()
            return redirect("author_detail", pk=author.pk)
    else:
        form = AuthorForm()

    return render(request, "authors/author_form.html", {"form": form})
```

---

## Step 2: Understand the flow

### 1. Check request type

```python id="g4r8dv"
if request.method == "POST":
```

👉 User submitted the form

---

### 2. Bind data to form

```python id="p9j3zn"
form = AuthorForm(request.POST)
```

👉 Connect user input to form

---

### 3. Validate data

```python id="q7w1xs"
if form.is_valid():
```

👉 Django checks rules automatically

---

### 4. Save data

```python id="v5k2la"
form.save()
```

👉 Adds to database

---

### 5. Redirect

```python id="r3f0yt"
return redirect("author_detail", pk=author.pk)
```

👉 Prevents duplicate submissions

---

## Step 3: Template stays the same

```html id="k8m3qp"
<form method="post">
  {% csrf_token %}
  {{ form.as_p }}
</form>
```

---

## Step 4: File uploads (from your project)

```python id="z1d9yx"
form = BookForm(request.POST, request.FILES)
```

👉 Needed when uploading images/files

---

## Real-world example

* User fills a form → submits
* System checks data → saves
* User is redirected

---

## 🎓 You Do

1. Create a `book_create` view
2. Handle POST requests
3. Save the book
4. Redirect to book detail page

---

## 🧠 Good habits

* Always check `request.method`
* Always use `form.is_valid()`
* Always redirect after POST
