# 🌐 Web Framework Integrations (Actix, Axum, Poem, Rocket, Warp)

Render Askama templates cleanly across any Rust web framework.

---

## ⚡ 1. Axum Integration

```rust
use axum::{
    http::StatusCode,
    response::{Html, IntoResponse, Response},
    routing::get,
    Router,
};
use askama::Template;

#[derive(Template)]
#[template(path = "index.html")]
struct IndexTemplate<'a> {
    title: &'a str,
}

async fn index_handler() -> Result<impl IntoResponse, AppError> {
    let tpl = IndexTemplate { title: "Axum App" };
    Ok(Html(tpl.render()?))
}

// Custom Error Handler for Axum
#[derive(Debug, thiserror::Error)]
enum AppError {
    #[error("Render error: {0}")]
    Render(#[from] askama::Error),
}

impl IntoResponse for AppError {
    fn into_response(self) -> Response {
        (StatusCode::INTERNAL_SERVER_ERROR, "Internal Error").into_response()
    }
}
```

---

## 🚀 2. Actix-Web Integration

```rust
use actix_web::{web::Html, Responder, get};
use askama::Template;

#[derive(Template)]
#[template(path = "home.html")]
struct HomeTemplate;

#[get("/")]
async fn home() -> Result<impl Responder, actix_web::Error> {
    let tpl = HomeTemplate;
    let body = tpl.render().map_err(actix_web::error::ErrorInternalServerError)?;
    Ok(Html::new(body))
}
```

---

## 📜 3. Rocket Integration

```rust
use rocket::{get, response::content::RawHtml};
use askama::Template;

#[derive(Template)]
#[template(path = "page.html")]
struct PageTemplate;

#[get("/")]
fn index() -> Result<RawHtml<String>, rocket::http::Status> {
    let tpl = PageTemplate;
    tpl.render()
       .map(RawHtml)
       .map_err(|_| rocket::http::Status::InternalServerError)
}
```

---

## 🔮 Simplified Alternative: `askama_web`

For automatic `IntoResponse` / `Responder` implementation across frameworks, use `#[derive(askama_web::WebTemplate)]`.
