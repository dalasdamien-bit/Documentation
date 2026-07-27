# 🔁 Control Flow, Loops & Pattern Matching

Askama supports full Rust-like logic control directly inside template tags.

---

## 🔄 For Loops & Loop Helpers

```jinja
<ul>
{% for user in users if user.is_active %}
  <li class="{% if loop.first %}first-item{% endif %}">
    {{ loop.index }}. {{ user.name }} {% if loop.last %}(End){% endif %}
  </li>
{% else %}
  <li>No active users available</li>
{% endfor %}
</ul>
```

### 📊 Loop Helper Variables
- `loop.index`: 1-based index (`1, 2, 3...`)
- `loop.index0`: 0-based index (`0, 1, 2...`)
- `loop.first`: `true` if first iteration
- `loop.last`: `true` if last iteration

---

## 🔀 Conditionals (`if`, `if let`, `is defined`)

### Standard `if` / `else if`
```jinja
{% if count == 0 %}
  Empty
{% elif count == 1 %}
  Single item
{% else %}
  {{ count }} items
{% endif %}
```

### Pattern Matching in `if let`
```jinja
{% if let Some(user) = current_user %}
  Welcome back, {{ user.name }}!
{% endif %}
```

### Check Variable Existence (`is defined` / `is not defined`)
```jinja
{% if custom_theme is defined %}
  Theme: {{ custom_theme }}
{% endif %}
```

---

## 🎯 Match Blocks (`match` / `when`)

Pattern match on Rust `enum`s, `Result`, `Option`, integers, or slices:

```jinja
{% match user_role %}
  {% when Role::Admin %}
    <span class="badge red">Admin</span>
  {% when Role::User with (id) %}
    <span>User #{{ id }}</span>
  {% else %}
    <span>Guest</span>
{% endmatch %}
```

### Multiple Alternative Patterns
```jinja
{% match number %}
  {% when 1 | 2 | 3 %} Low number
  {% when 10..=20 %} Mid range
  {% else %} Other
{% endmatch %}
```

---

## ❓ Try Operator (`?`)

Unwrap `Result` expressions directly in templates:

```jinja
{{ fetch_data()? }}
{% let content = parse_json()? %}
```
*If an `Err` is returned, template rendering halts immediately and returns an `askama::Error::Custom`.*
