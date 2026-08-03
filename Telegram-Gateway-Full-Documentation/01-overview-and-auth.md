# ✈️ Telegram Gateway API: Overview & Auth

The **Telegram Gateway API** delivers automated SMS/Telegram verification messages and one-time passwords (OTPs) to users registered on Telegram.

---

## 📢 Recent Changes (February 26, 2025)

- **TTL Range Updated**: `ttl` parameter in `sendVerificationMessage` now supports **30 to 3,600 seconds**.
- **Automatic Refund Guarantee**: If a message is **not delivered** within the specified `ttl`, the request fee is automatically refunded. Delivered/read messages are not refunded.
- **New Types & Fields**: Added `is_refunded` boolean to `RequestStatus`. Added `delivered` and `expired` statuses to `DeliveryStatus`.
- **Revocation Rule**: `revokeVerificationMessage` will not delete messages that have already been delivered or read.

---

## 🌐 Base URL & Request Formats

All queries must be served over **HTTPS**:

```
https://gatewayapi.telegram.org/METHOD_NAME
```

### Supported Encoding & Methods
- **HTTP Methods**: `GET` and `POST`
- **Parameter Pass-through Options**:
  1. `application/json`
  2. `application/x-www-form-urlencoded`
  3. URL Query String
- **Character Encoding**: Strictly **UTF-8**
- **Case Sensitivity**: Method names are case-insensitive.

---

## 🔑 Authorization

Obtain your access token in the Telegram Gateway account settings. Pass it in **every** request via:

1. **HTTP Header (Recommended)**:
   ```http
   Authorization: Bearer <YOUR_API_TOKEN>
   ```
2. **URL Query Parameter**:
   ```
   ?access_token=<YOUR_API_TOKEN>
   ```
