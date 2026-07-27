# 🏗️ Template Inheritance, Includes & Macros

Organize complex template hierarchies with layout inheritance, modular includes, and Jinja macros.

---

## 🏛️ Template Inheritance (`extends`)

### Base Layout (`templates/base.html`)
```html
<!DOCTYPE html>
<html>
<head>
  <title>{% block title %}{{ title }} - My Site{% endblock %}</title>
</head>
<body>
  <main>
    {% block content %}<p>Default Content</p>{% endblock %}
  </main>
</body>
</html>
```

### Child Page (`templates/page.html`)
```jinja
{% extends "base.html" %}

{% block title %}Dashboard - {{ super() }}{% endblock %}

{% block content %}
  <h1>Dashboard Overview</h1>
  <p>Welcome to the portal!</p>
{% endblock %}
```

---

## 🧩 Template Includes (`include`)

Split large templates into smaller, modular files. Included templates inherit full context:

```jinja
{% for user in user_list %}
  {% include "partials/user_card.html" %}
{% endfor %}
```

---

## 🪄 Macros & Named Arguments

Define reusable UI components:

```jinja
{% macro button(label, variant = "primary", size = 16) %}
  <button class="btn btn-{{ variant }}" style="font-size: {{ size }}px">
    {{ label }}
  </button>
{% endmacro %}

{# Call positionally or by named arguments #}
{{ button("Save") }}
{{ button(label = "Delete", variant = "danger") }}
```

---

## 🧱 Macro Call Blocks (`call` & `caller()`)

Call blocks allow passing rich HTML bodies into macros:

```jinja
{% macro modal(title) %}
  <div class="modal">
    <h2>{{ title }}</h2>
    <div class="modal-body">
      {% if caller is defined %}
        {{ caller() }}
      {% endif %}
    </div>
  </div>
{% endmacro %}

{% call modal("Confirm Action") %}
  <p>Are you sure you want to proceed?</p>
  <button>Yes</button>
{% endcall %}
```
