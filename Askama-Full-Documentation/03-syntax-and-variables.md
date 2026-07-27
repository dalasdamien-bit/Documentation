# 🔑 Variables, Assignments & Scope Rules

Askama templates access variables directly from the Rust struct context or local template declarations.

---

## 📌 Variable Access & Dot Notation

```jinja
{{ name }}             {# Access struct field 'name' #}
{{ user.profile.bio }} {# Access nested struct field or zero-arg method #}
{{ crate::MAX_LIMIT }}  {# Access Rust constant defined in crate root #}
```

---

## 📝 Declaring Variables

### 1. Basic Assignment (`let` / `set`)
```jinja
{% let name = user.name %}
{% let mut count = 0 %}
```

### 2. Block-Computed String Assignment
```jinja
{% let header %}
  <h1>{{ title }} - {{ category }}</h1>
{% endlet %}
```

### 3. Delayed Conditional Assignment (`decl` / `declare`)
*Note: In Askama v0.16+, uninitialized variables must use `decl`.*

```jinja
{% decl status %}
{% if is_admin %}
  {% let status = "Administrator" %}
{% else %}
  {% let status = "Standard User" %}
{% endif %}
{{ status }}
```

---

## ➕ Compound Assignments (`mut`)

Mutating declared variables uses `{% mut var OP val %}`:

```jinja
{% let mut counter = 0 %}
{% for i in 1..=5 %}
  {% mut counter += i %}
  Step {{ loop.index }}: total is {{ counter }}
{% endfor %}
```

---

## 🛡️ Borrowing Rules Matrix

When initializing variables in templates, Askama automatically decides whether to place the value behind a reference (`&`):

| Variable Source / Expression | Behind Reference? (`&`) | Reason |
| :--- | :--- | :--- |
| Complex expression (`x + 2`) | ❌ NO | Temporary value |
| Local template variable | ❌ NO | Moved or copied |
| Filtered value (`x | capitalize`) | ❌ NO | Fresh output string |
| Struct field (`x.y`) | ✅ YES | Prevents taking ownership of struct field |
| Try operator (`x?`) | ❌ NO | Unwrapped value |

---

## 🔀 Type Conversion (`as`)

Cast primitive types directly inside expressions:

```jinja
{{ (count as f64) / 100.0 }}
```
