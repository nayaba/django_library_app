# 🛠️ SETUP

<h1>
  <span class="headline">Django CRUD App</span>
  <span class="subhead">Setup</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to create and run a Django project locally.

---

## Step 1: Create a project folder

Open your terminal and run:

```bash
mkdir library_project
cd library_project
```

---

## Step 2: Create a virtual environment

```bash
python -m venv venv
```

Activate it:

**Mac/Linux:**

```bash
source venv/bin/activate
```

**Windows:**

```bash
venv\Scripts\activate
```

> 💡 A virtual environment keeps your project dependencies separate.

---

## Step 3: Install Django

```bash
pip install django psycopg2-binary
```

---

## Step 4: Create the Django project

```bash
django-admin startproject library_project .
```

> 💡 The `.` puts the project files in the current folder.

---

## Step 5: Create the app

```bash
python manage.py startapp main_app
```

---

## Step 6: Register the app

Open `settings.py` and add:

```python
INSTALLED_APPS = [
    ...
    'main_app',
]
```

---

## Step 7: Run the server

```bash
python manage.py runserver
```

Visit:

```
http://127.0.0.1:8000/
```

You should see the Django welcome page 🎉

---

## Step 8: Confirm your project works

Try this command:

```bash
python manage.py migrate
```

👉 This sets up your database.

---

## Step 9: Create a superuser (optional but recommended)

```bash
python manage.py createsuperuser
```

Then visit:

```
http://127.0.0.1:8000/admin/
```

---

## Step 10: Understand your project structure

You should now have:

```
library_project/
│
├── library_project/   # project settings
├── main_app/          # your app
├── manage.py          # command center
```

> 💡 Think of:
>
> * project = entire system
> * app = one feature inside the system

---

## 🎓 You Do

1. Create your project and app
2. Run the server
3. Visit the admin page
4. Take a screenshot of the Django welcome page

---

## 🧠 Good habits

* Always activate your virtual environment
* Run `pip freeze > requirements.txt` after installing packages
* Use clear folder names (`main_app`, not `app1`)

---

<div style="display: flex; justify-content: space-between;">

  <!-- Previous Lesson -->
  <a href="../README.md">⬅ Previous</a>

  <!-- Next Lesson -->
  <a href="../concepts/README.md">Next: Concepts ➡</a>

</div>
