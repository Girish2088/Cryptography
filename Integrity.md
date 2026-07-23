# 🛡️ Integrity

**Integrity** ensures that data has **not been modified** during storage or transmission.

It answers the question:

> **"Has the data changed?"**

Integrity is commonly achieved using **Hash Functions**.

---

# Hashing

A hash function converts data into a fixed-length value called a **Hash**.

```text
File
 ↓
SHA-256
 ↓
Hash
```

The hash acts like a **digital fingerprint** of the data.

---

## Properties of Hashing

- Same input → Same output
- Small input change → Completely different hash (Avalanche Effect)
- Fixed output length
- One-way function (cannot recover original data)

---

## SHA-256

- Produces a **256-bit** hash
- Output length: **64 hexadecimal characters**
- Commonly used to verify file integrity

Example:

```bash
sha256sum file.iso
```

---

## SHA-512

- Produces a **512-bit** hash
- Output length: **128 hexadecimal characters**
- Same purpose as SHA-256 with a longer hash

Example:

```bash
sha512sum file.iso
```

---

# File Integrity Example

Official Website:

```text
SHA256

ABC123...
```

Your Computer:

```bash
sha256sum kali-linux.iso
```

Result:

```text
ABC123...
```

✅ Same hash → File is original.

❌ Different hash → File modified or corrupted.

---

# Common Uses

- File integrity verification
- Software downloads
- Password storage
- Digital signatures

---

# Interview Questions

### What is Integrity?

> Integrity ensures that data has not been modified.

### How is Integrity verified?

> By comparing the calculated hash with the original hash.

### Can hashing recover the original data?

> No. Hashing is a one-way function.

---

# One-Line Revision

```text
Integrity → Detects data modification

Hash → Digital fingerprint

SHA-256 → 256-bit hash

SHA-512 → 512-bit hash

Same hash → Original data

Different hash → Modified or corrupted
```

---

# Memory Hook

```text
File
 ↓
Hash
 ↓
Compare

Same Hash

↓

Original File

Different Hash

↓

Modified File
```
