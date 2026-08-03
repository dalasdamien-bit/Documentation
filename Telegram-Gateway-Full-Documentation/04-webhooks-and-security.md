# 🔔 Webhooks & HMAC-SHA256 Verification

When a `callback_url` is provided, Telegram posts delivery reports as HTTP `POST` requests containing a `RequestStatus` JSON body.

---

## 🔁 Webhook Delivery Rules

1. **Acknowledge with HTTP 200**: Your server **must** return an HTTP `200` status.
2. **Retries**: Any non-200 response triggers up to **10 retries** with increasing backoff delays before dropping the report.

---

## 🛡️ Checking Report Integrity

Every webhook POST includes two security headers:
- `X-Request-Timestamp`: Unix timestamp when the report was submitted.
- `X-Request-Signature`: Hexadecimal HMAC-SHA256 signature.

### 📐 Verification Formula

```python
data_check_string = X_Request_Timestamp + '
' + raw_post_body
secret_key = SHA256(api_token)
expected_signature = Hex(HMAC_SHA256(data_check_string, secret_key))

is_valid = (expected_signature == X_Request_Signature)
```

> 💡 **Replay Attack Protection**: Always verify that `X-Request-Timestamp` is within a reasonable tolerance (e.g. within 5 minutes of current time).
