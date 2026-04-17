# Template Basics (Loops & Conditionals)

**Learning objective:** By the end of this lesson, students will be able to use loops and conditionals in Django templates to display dynamic content.

---

## Why this matters

Templates are not just HTML — they can **think**.

👉 Show lists
👉 Show/hide content
👉 Handle empty data

---

## Step 1: Loop through data

```html id="q3k7yt"
{% for a in authors %}
  <p>{{ a.first_name }} {{ a.last_name }}</p>
{% endfor %}
```

👉 This repeats for each author

---

## Step 2: Add an empty state

```html id="6r2z4c"
{% for a in authors %}
  <p>{{ a.first_name }}</p>
{% empty %}
  <p>No authors found.</p>
{% endfor %}
```

👉 This runs if there is no data

---

## Step 3: Use conditionals

```html id="9p1h4d"
{% if a.is_best_seller %}
  ⭐ Best Seller
{% endif %}
```

👉 Only shows when true

---

## Step 4: If / else

```html id="3z7g2w"
{% if author.is_best_seller %}
  <p>Best-selling</p>
{% else %}
  <p>Not best-selling</p>
{% endif %}
```

---

## Step 5: Combine loop + condition

```html id="2c8nqk"
{% for a in authors %}
  <p>
    {{ a.first_name }}
    {% if a.is_best_seller %}⭐{% endif %}
  </p>
{% endfor %}
```

---

## Step 6: Access related data

From your project:

```html id="8g4xkp"
{% for book in books %}
  <p>{{ book.title }}</p>
{% endfor %}
```

👉 This shows books for one author

---

## Real-world example

Think of a dashboard:

* Loop → show all records
* If → highlight important ones
* Empty → show “no data” message

---

## 🎓 You Do

1. Update your author list:

   * Add ⭐ for best sellers

2. Add an empty message:

```html id="9v7k3n"
No authors yet.
```

3. On author detail page:

   * Show all books
   * Show message if no books

---

## 🧠 Good habits

* Keep templates simple
* Avoid heavy logic in templates
* Always handle empty data

