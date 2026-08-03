# 🧩 Data Types & Object Schemas

All response objects are represented as standard JSON objects. Integer values fit safely within 32-bit signed integers.

---

## 1. `RequestStatus`

Represents the state and cost of a verification request.

| Field | Type | Description |
| :--- | :--- | :--- |
| `request_id` | String | Unique request ID. |
| `phone_number` | String | Target E.164 phone number. |
| `request_cost` | Float | Cost incurred for this request. |
| `is_refunded` | Boolean | *Optional*. `true` if fee was refunded (e.g. expired/undelivered in TTL). |
| `remaining_balance` | Float | *Optional*. Remaining credit balance. |
| `delivery_status` | `DeliveryStatus` | *Optional*. Message delivery state. |
| `verification_status` | `VerificationStatus`| *Optional*. Code entry verification state. |
| `payload` | String | *Optional*. Echoed custom payload string (0-256 bytes). |

---

## 2. `DeliveryStatus`

Represents the physical delivery state of the Telegram message.

| Field | Type | Description |
| :--- | :--- | :--- |
| `status` | String | Delivery state enum value: |
| | | - `sent`: Sent to recipient's device(s). |
| | | - `delivered`: Delivered to recipient's device(s). |
| | | - `read`: Read by the recipient. |
| | | - `expired`: Expired without delivery/read within TTL. |
| | | - `revoked`: Message revoked by sender. |
| `updated_at` | Integer | Unix timestamp when status last changed. |

---

## 3. `VerificationStatus`

Represents the OTP validation state.

| Field | Type | Description |
| :--- | :--- | :--- |
| `status` | String | Verification state enum value: |
| | | - `code_valid`: OTP code matches. |
| | | - `code_invalid`: OTP code incorrect. |
| | | - `code_max_attempts_exceeded`: Max retries exceeded. |
| | | - `expired`: Code expired and unusable. |
| `updated_at` | Integer | Unix timestamp when verification state updated. |
| `code_entered` | String | *Optional*. Last code entered by the user. |
