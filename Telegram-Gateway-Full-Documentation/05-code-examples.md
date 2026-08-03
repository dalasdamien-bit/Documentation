# 💻 Integration Code Snippets

---

## ⚡ 1. cURL Quick Commands

```bash
# 1. Send OTP
curl -X POST https://gatewayapi.telegram.org/sendVerificationMessage   -H "Authorization: Bearer YOUR_TOKEN"   -H "Content-Type: application/json"   -d '{
    "phone_number": "+14155552671",
    "code": "849201",
    "ttl": 300
  }'

# 2. Check Code Status
curl -X POST https://gatewayapi.telegram.org/checkVerificationStatus   -H "Authorization: Bearer YOUR_TOKEN"   -H "Content-Type: application/json"   -d '{
    "request_id": "req_8f3a91b2c4e5",
    "code": "849201"
  }'
```

---

## 🐍 2. Python Requests Example

```python
import requests

API_TOKEN = "YOUR_GATEWAY_TOKEN"
BASE_URL = "https://gatewayapi.telegram.org"

headers = {
    "Authorization": f"Bearer {API_TOKEN}",
    "Content-Type": "application/json"
}

# Send verification message
response = requests.post(f"{BASE_URL}/sendVerificationMessage", headers=headers, json={
    "phone_number": "+14155552671",
    "code_length": 6,
    "ttl": 180
})

result = response.json()
if result.get("ok"):
    request_id = result["result"]["request_id"]
    print(f"Message Sent! Request ID: {request_id}")
else:
    print(f"Error: {result.get('error')}")
```
