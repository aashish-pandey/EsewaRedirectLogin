# 💸 eSewa Auto-Payment Launcher

A lightweight HTML + JavaScript tool to auto-submit a payment form to eSewa using query parameters.  
Useful for quickly testing or integrating eSewa in MVPs or static sites.

---

## 🚀 What It Does

- Parses URL parameters like `amount`, `product_code`, `secret`, etc.
- Fills in hidden eSewa payment fields
- Generates an HMAC-SHA256 `signature` using CryptoJS
- Auto-submits the form to eSewa’s sandbox endpoint

---

## 🧪 Example Usage

URL to open this page with auto-filled and auto-submitted form:

```
https://yourdomain.com/esewa.html?amount=400&tax_amount=0&product_code=EPAYTEST&secret=8gBm/:EnhH.1/q
```

This will:
- Fill form fields
- Generate the required signature
- Submit to `https://rc-epay.esewa.com.np/api/epay/main/v2/form`

---

## 🔧 Required Query Parameters

| Param           | Description                            |
|-----------------|----------------------------------------|
| `amount`        | Base amount to be paid                 |
| `tax_amount`    | Any tax amount (0 if none)             |
| `product_code`  | eSewa product code (e.g. `EPAYTEST`)   |
| `secret`        | Secret key to sign the payload         |

---

## 🔐 Signature Generation

The form signs these fields:

```
total_amount,transaction_uuid,product_code
```

Using the formula:

```js
CryptoJS.HmacSHA256(
  "total_amount=... ,transaction_uuid=... ,product_code=...",
  secret
)
```

Encoded with Base64 before sending to eSewa.

---

## ⚠️ Disclaimer

This project is for **educational and testing** purposes only.

> Do NOT expose your real `secret` key in a production URL.  
Use server-side signing for live environments.

---

## 📦 Dependencies

- [CryptoJS](https://cdnjs.com/libraries/crypto-js) (loaded via CDN)

---

## 🧑‍💻 Author

**Aashish Prashad Pandey**  
Built for developers in Nepal 🇳🇵 to simplify eSewa test integrations.
