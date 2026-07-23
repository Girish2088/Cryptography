# HMAC (Hash-based Message Authentication Code)

## What is HMAC?

HMAC (Hash-based Message Authentication Code) is a cryptographic technique that combines a **secret key** with a **hashing algorithm** (such as SHA-256 or SHA-512).

It provides:

- **Integrity** → Detects if the data has been modified.
- **Authentication** → Verifies that the message came from someone who knows the secret key.

Unlike normal hashing, HMAC requires both the sender and receiver to share the **same secret key**.

---

# Why Do We Need HMAC?

A normal hash only provides integrity.

Example:

```
Message
   ↓
SHA-256
   ↓
Hash
```

The problem is that **anyone** can calculate a SHA-256 hash.

An attacker could:

1. Modify the message.
2. Generate a new SHA-256 hash.
3. Send both the modified message and the new hash.

The receiver would not know who actually created the hash.

---

# How HMAC Works

Both sender and receiver share a secret key.

```
Message
   +
Secret Key
      ↓
HMAC (SHA-256)
      ↓
Authentication Code
```

The sender sends:

```
Message
+
HMAC
```

The receiver performs the same HMAC calculation using the same secret key.

If both HMAC values match:

- ✅ Message was not modified.
- ✅ Message came from someone who knows the secret key.

---

# Example

Shared Secret Key

```
mySecret123
```

Sender

```
Message
   +
Secret Key
      ↓
HMAC-SHA256
      ↓
Send:
Message + HMAC
```

Receiver

```
Received Message
        +
Same Secret Key
        ↓
HMAC-SHA256
        ↓
Compare

Match
↓

Valid
```

---

# Where is HMAC Used?

HMAC is commonly used wherever two trusted parties share a secret key.

Examples include:

- HTTPS / TLS
- REST APIs
- JWT (JSON Web Tokens)
- VPNs
- AWS Request Signing
- Secure communication protocols

---

# Real-World Example (API Authentication)

Suppose your application sends a request to a server.

```
Amount = ₹5000
```

Instead of sending only the request, the client also generates an HMAC.

```
Amount
   +
Secret Key
      ↓
HMAC
```

The client sends:

```
Amount = ₹5000

HMAC = X7A92BC...
```

The server calculates the HMAC using the same secret key.

If the calculated HMAC matches the received HMAC:

✅ Request is authentic.

If someone changes the request to:

```
Amount = ₹50000
```

the HMAC will no longer match.

The server immediately rejects the request.

---

# Hash vs HMAC

| Feature | Hash (SHA-256) | HMAC |
|---------|----------------|------|
| Uses Secret Key | ❌ No | ✅ Yes |
| Provides Integrity | ✅ Yes | ✅ Yes |
| Provides Authentication | ❌ No | ✅ Yes |
| Anyone Can Generate | ✅ Yes | ❌ Only users with the secret key |

---

# Interview Questions

### What is HMAC?

> HMAC (Hash-based Message Authentication Code) is a cryptographic mechanism that combines a secret key with a hashing algorithm to provide both integrity and authentication.

---

### Why use HMAC instead of a normal hash?

A normal hash only detects data modification.

HMAC also verifies that the message came from someone who knows the shared secret key.

---

### Which hashing algorithms are commonly used with HMAC?

- HMAC-SHA256
- HMAC-SHA512

---

# Memory Hook

```
Hash

↓

Integrity

HMAC

↓

Integrity
+
Authentication
```

---

# One-Line Revision

```
HMAC = Hash + Secret Key

Provides:
• Integrity
• Authentication

Commonly used with:
• SHA-256
• SHA-512
```
