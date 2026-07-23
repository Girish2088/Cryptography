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

# Understanding Keys in Digital Signatures

The same Public Key and Private Key used for encryption are also used for Digital Signatures.

The difference is **how they are used**.

## Encryption

```
Public Key
    ↓
Encrypt Data
    ↓
Private Key
    ↓
Decrypt Data
```

Purpose:

```
Confidentiality

(Hide the data)
```

---

## Digital Signature

```
Private Key
    ↓
Sign Hash
    ↓
Digital Signature
    ↓
Public Key
    ↓
Verify Signature
```

Purpose:

```
Authenticity

(Prove who created the data)
```

---

## Easy Way to Remember

```
Encryption

↓

Can only the receiver read it?

------------------------------

Digital Signature

↓

Did the real sender create it?
```

The same key pair is used in both cases.

Only the purpose changes.

---

# Digital Signatures

A Digital Signature proves:

- Authenticity (Who created the file)
- Integrity (File has not been modified)
- Non-Repudiation (Sender cannot deny creating it)

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

# Receiver Verification

The receiver performs two operations.

### Step 1

Generate a new hash from the received file.

```
report.pdf

↓

SHA-256

↓

ABC123XYZ
```

---

### Step 2

Verify the Digital Signature using the sender's Public Key.

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
Hash from File

==

Hash from Digital Signature
```

If both hashes are equal:

```
✓ File was not modified.

✓ Signature was created using the sender's Private Key.

✓ Therefore the sender is authentic.
```

If they are different:

```
✗ File was modified

OR

✗ Signature is invalid

OR

✗ Wrong Public Key was used
```

---

# Real-Life Example

Suppose Girish sends:

```
report.pdf

+

Digital Signature
```

Receiver:

```
Creates hash of report.pdf

↓

Verifies Digital Signature using Girish's Public Key

↓

Compares both hashes

↓

If Equal

↓

Trust the file
```

---

# Where are Digital Signatures Used?

- HTTPS
- Software Downloads
- Git Commit Signing
- PDF Signing
- Email Signing
- Code Signing

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

CA Signature
```

A Certificate **does not** contain the Private Key.

---

# Why Do We Need Certificates?

Anyone can generate:

```
Public Key

Private Key
```

A hacker could also generate a key pair and claim:

```
"I am google.com"
```

How does your browser know whether that Public Key really belongs to Google?

Certificates solve this problem.

They bind a Public Key to a verified owner.

---

# Certificate Authority (CA)

A Certificate Authority (CA) is a trusted third party.

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

CA signs the Certificate using its Private Key

↓

Certificate Issued
```

---

# Browser Verification

When you visit:

```
https://google.com
```

The browser receives Google's certificate.

Then it checks:

```
Was this certificate signed by a trusted CA?
```

The browser already contains the Public Keys of trusted Certificate Authorities.

It uses the CA's Public Key to verify the CA's Digital Signature.

If the verification succeeds:

```
✓ Certificate is trusted

↓

✓ Trust Google's Public Key

↓

✓ Secure HTTPS Connection
```

If verification fails:

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

But the attacker **cannot obtain a valid CA signature for google.com**.

Without a trusted CA signature,

the browser refuses to trust the attacker's certificate.

---

# Complete Picture

```
Encryption
        ↓
Confidentiality

----------------------------

Hashing
        ↓
Integrity

----------------------------

Digital Signature
        ↓
Authenticity
Integrity
Non-Repudiation

----------------------------

Certificate
        ↓
Authentication
Identity Verification

----------------------------

Certificate Authority
        ↓
Trust
```

---

# Interview Questions

### What is a Digital Signature?

A hash of data signed using the sender's Private Key.

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

----------------------

SHA
↓

Detect Changes
(Integrity)

----------------------

Digital Signature
↓

Who Created It?
(Authenticity)

----------------------

Certificate
↓

Who Owns This Public Key?
(Authentication)

----------------------

Certificate Authority
↓

Who Can We Trust?
(Trust)
```
