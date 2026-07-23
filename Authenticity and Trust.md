# Authenticity & Trust

Until now we have learned:

```
Confidentiality
↓

Encryption (AES, RSA, ECC)

Integrity
↓

Hashing (SHA-256, SHA-512, HMAC)

Authentication
↓

Passwords
SSH Keys
Certificates
```

Now we'll learn how to answer these questions:

- Who created this file?
- Has this file been modified?
- Can I trust this website?

These are solved using:

- Digital Signatures
- Certificates
- Certificate Authorities (CA)

---

# Digital Signatures

A Digital Signature proves:

- Who created the data (Authenticity)
- The data has not been modified (Integrity)
- The sender cannot deny sending it (Non-Repudiation)

---

## How It Works

### Step 1

Create a hash of the file.

```
report.pdf

↓

SHA-256

↓

ABC123XYZ
```

---

### Step 2

Encrypt the hash using the sender's Private Key.

```
Hash

↓

Private Key

↓

Digital Signature
```

---

### Step 3

Send:

```
report.pdf

+

Digital Signature
```

---

## Receiver Verification

Receiver performs two operations.

### Step 1

Generate a new hash.

```
report.pdf

↓

SHA-256

↓

ABC123XYZ
```

---

### Step 2

Decrypt the Digital Signature using the sender's Public Key.

```
Digital Signature

↓

Public Key

↓

ABC123XYZ
```

---

### Step 3

Compare both hashes.

```
Hash 1 == Hash 2

↓

YES

↓

✓ File is original
✓ File was not modified
✓ File was signed by the owner
```

---

# Important Difference

## Encryption

```
Public Key

↓

Encrypt

↓

Private Key

↓

Decrypt
```

Purpose:

```
Confidentiality
```

---

## Digital Signature

```
Private Key

↓

Sign

↓

Public Key

↓

Verify
```

Purpose:

```
Authenticity

Integrity

Non-Repudiation
```

Notice that the keys are the same.

Only their direction changes.

---

# Real-World Uses

- HTTPS
- Software Downloads
- Git Commit Signing
- Code Signing
- PDF Signing
- Email Signing

---

# Certificates

A Certificate is a digital identity card.

It proves that a Public Key belongs to a specific owner.

Example:

```
Owner:
google.com

Public Key:
ABC123XYZ

Issued By:
Google Trust Services

Expiry:
12 Jan 2027

Signature:
CA Signature
```

A Certificate does NOT contain the Private Key.

---

# Why Do We Need Certificates?

Anyone can generate:

```
Public Key

Private Key
```

A hacker could create keys and claim:

```
"I am google.com"
```

How can your browser know?

Certificates solve this problem.

They bind a Public Key to a verified owner.

---

# Certificate Authority (CA)

A Certificate Authority is a trusted third party.

Its job is to verify that a Public Key really belongs to the claimed owner before issuing a certificate.

Examples:

- Let's Encrypt
- DigiCert
- Sectigo
- GlobalSign

---

# How CA Works

```
Website Owner

↓

Generates Public & Private Key

↓

Requests Certificate

↓

CA verifies domain ownership

↓

CA signs the Certificate

↓

Certificate Issued
```

---

# Browser Verification

When visiting:

```
https://google.com
```

The browser receives Google's certificate.

It checks:

```
Was this certificate signed by a trusted CA?
```

If YES

```
✓ Trust this Public Key

↓

Secure HTTPS Connection
```

If NO

```
❌ Your connection is not private

NET::ERR_CERT_AUTHORITY_INVALID
```

---

# Why MITM Attack Fails

An attacker can generate:

```
Public Key

Private Key
```

But the attacker cannot obtain a valid CA signature for:

```
google.com
```

Without a trusted CA signature,

the browser refuses to trust the attacker's certificate.

---

# Complete Picture

```
Encryption

↓

Confidentiality

-------------------------

Hashing

↓

Integrity

-------------------------

Digital Signature

↓

Authenticity

Integrity

Non-Repudiation

-------------------------

Certificates

↓

Authentication

Identity Verification

-------------------------

Certificate Authority

↓

Trust
```

---

# Interview Questions

### What is a Digital Signature?

A hash of data encrypted using the sender's Private Key.

---

### Which key signs a Digital Signature?

Private Key.

---

### Which key verifies a Digital Signature?

Public Key.

---

### What does a Digital Signature provide?

- Authenticity
- Integrity
- Non-Repudiation

---

### What is a Certificate?

A digital identity card that binds a Public Key to its owner.

---

### Does a Certificate contain the Private Key?

No.

Only the Public Key.

---

### What is a Certificate Authority (CA)?

A trusted organization that verifies ownership of a Public Key and signs Certificates.

---

### Why do browsers trust Certificates?

Because browsers and operating systems already contain the Public Keys of trusted Certificate Authorities.

---

# Memory Hook

```
AES
↓

Hide Data
(Confidentiality)

--------------------

SHA
↓

Detect Changes
(Integrity)

--------------------

Digital Signature
↓

Who Sent It?
(Authenticity)

--------------------

Certificate
↓

Who Owns This Public Key?
(Authentication)

--------------------

Certificate Authority
↓

Who Can We Trust?
(Trust)
```
