# 🚀 Telegram Gateway API Method Reference

Quick-reference for the 4 core API methods.

---

## 1. `sendVerificationMessage`
Sends a OTP / verification code to a Telegram user. Charges apply based on delivery. **Free when sending to your own registered account phone number.**

### Parameters
| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `phone_number` | String | **Yes** | Destination number in E.164 format (e.g. `+14155552671`). |
| `request_id` | String | Optional | ID from `checkSendAbility`. If supplied, this dispatch is free. |
| `sender_username`| String | Optional | Channel username owned & verified by the token owner. |
| `code` | String | Optional | Custom numeric OTP (4-8 digits). If set, `code_length` is ignored. |
| `code_length` | Integer | Optional | Length (4-8) for Telegram auto-generated code. |
| `callback_url` | String | Optional | HTTPS webhook URL (0-256 bytes) for delivery reports. |
| `payload` | String | Optional | Custom metadata string (0-128 bytes) returned in callbacks. |
| `ttl` | Integer | Optional | Time-To-Live in seconds (30 - 3600). Auto-refunded if undelivered in TTL. |

**Returns**: `RequestStatus` object on success.

---

## 2. `checkSendAbility`
Checks if a verification message can be delivered to the target phone number before sending.

### Parameters
| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `phone_number` | String | **Yes** | Target E.164 phone number. |

- If sendable, incurs fee and returns a `RequestStatus` containing a `request_id`.
- Re-using this `request_id` in `sendVerificationMessage` will be **free of charge**.

---

## 3. `checkVerificationStatus`
Checks delivery/verification progress or validates an OTP entered by the user.

### Parameters
| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `request_id` | String | **Yes** | Unique request identifier. |
| `code` | String | Optional | User-submitted OTP string to verify. |

**Returns**: `RequestStatus` object with updated `verification_status`.

---

## 4. `revokeVerificationMessage`
Revokes a pending verification message.

### Parameters
| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `request_id` | String | **Yes** | Unique request identifier. |

**Returns**: `true` boolean if revocation request was received. *(Note: Delivered or read messages cannot be deleted).*
