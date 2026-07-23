# 🔒 Confidentiality

**Confidentiality** means keeping data secret so that **only the intended receiver can read it**.

Encryption is used to protect data while it travels across a network.

---

# Symmetric Encryption

## AES (Advanced Encryption Standard)

Uses **one shared key** for both encryption and decryption.

### Characteristics

- One shared key
- Very fast and efficient
- Used to encrypt the actual data being transferred

---

## Example

```text
Browser creates AES key
        ↓
AES key encrypts messages
        ↓
Bank server uses the same AES key to decrypt
```

---

# Asymmetric Encryption

## RSA / ECC

Uses **two keys**:

- Public Key
- Private Key

### Characteristics

- Public Key can be shared with everyone.
- Private Key must remain secret.
- Slower than AES.
- Used to securely exchange secret keys.

---

## Example

```text
Bank Server

│
├── Public Key  → Shared with Browser
└── Private Key → Stays on Bank Server
```

### Browser Process

1. Browser creates an AES key.
2. Browser encrypts the AES key using the Bank's Public Key.
3. Browser sends the encrypted AES key to the Bank.
4. Bank decrypts the AES key using its Private Key.
5. Both now share the same AES key.

---

## Result

```text
Browser ⇄ AES ⇄ Bank Server
```

RSA/ECC solve the problem of **securely sharing the secret AES key**.

After the key exchange, **AES is used for all further communication** because it is much faster.

---

# Why HTTPS Uses Both

```text
Browser
      │
Creates AES Key
      │
Encrypts AES Key using RSA/ECC
      │
────────────►
      │
Server decrypts AES Key
using Private Key
      │
Both share the same AES Key
      │
AES encrypts all communication
```

---

# Symmetric vs Asymmetric Encryption

| Symmetric Encryption | Asymmetric Encryption |
| -------------------- | --------------------- |
| One shared key | Public & Private keys |
| Very fast | Slower |
| AES | RSA / ECC |
| Encrypts actual data | Securely exchanges the AES key |

---

# Interview Questions

### What is Confidentiality?

> Confidentiality ensures that only authorized users can access and read data.

---

### Why doesn't HTTPS use only RSA?

> RSA/ECC are computationally expensive. They are used only to securely exchange the AES key. AES is then used to encrypt the actual communication because it is much faster.

---

# One-Line Revision

```text
Confidentiality → Keeps data secret

AES → Fast symmetric encryption

RSA → Public/Private key encryption

ECC → Modern asymmetric encryption with smaller keys

HTTPS → RSA/ECC exchange the AES key, AES encrypts the data
```

---

# Memory Hook

```text
RSA / ECC

↓

Securely Share AES Key

↓

AES

↓

Encrypt Everything
```
