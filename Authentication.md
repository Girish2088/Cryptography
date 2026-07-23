# Authentication

Authentication is the process of verifying the identity of a user, device, or server before allowing access.

Common authentication methods include:

- Passwords
- SSH Keys
- Certificates

---

# Password Authentication

Password Authentication is the most common way to verify a user's identity.

The user enters a username and password.

If the password matches the one stored by the server, access is granted.

---

## How It Works

```
User

↓

Username + Password

↓

Server

↓

Password Verified

↓

Login Successful
```

---

## Example

```bash
ssh username@192.168.1.20
```

Server asks:

```
Password:
```

Enter the correct password.

If correct:

```
Login Successful
```

---

## Where is it Used?

- Linux Login
- Windows Login
- SSH Login
- Websites
- Email Accounts
- Database Login

---

## Advantages

- Easy to use
- No setup required
- Supported almost everywhere

---

## Disadvantages

- Weak passwords can be guessed.
- Can be stolen through phishing.
- Can be brute-forced.
- Users often reuse the same password.

---

## Good Password Practices

- Use strong and long passwords.
- Don't reuse passwords.
- Use a Password Manager.
- Enable Multi-Factor Authentication (MFA).

---

# Certificates

A Certificate is a digital identity card.

It proves that a public key belongs to a specific person, company, or server.

Certificates are mainly used on the Internet to verify the identity of websites and servers.

---

## Why Do We Need Certificates?

Anyone can generate a Public Key and Private Key.

For example, a hacker can create:

```
Public Key
Private Key
```

Then claim:

```
"I am google.com"
```

How can your browser know if that public key really belongs to Google?

Certificates solve this problem.

---

## What Does a Certificate Contain?

A certificate usually contains:

- Owner Name (Domain/Organization)
- Public Key
- Certificate Authority (CA)
- Expiry Date
- CA Digital Signature

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
CA Digital Signature
```

---

## How It Works

```
Website

↓

Sends Certificate

↓

Browser Receives Certificate

↓

Checks CA Signature

↓

If Valid

↓

Trust Website
```

---

## Real-Life Example

Imagine someone says:

```
"I am a Police Officer."
```

You ask for an ID Card.

The ID card proves:

- Name
- Organization
- Government Signature

Similarly, a Certificate proves:

- Owner
- Public Key
- Trusted CA Signature

---

## Where are Certificates Used?

- HTTPS Websites
- VPN
- Email Security
- Enterprise Wi-Fi
- Software Signing
- TLS/SSL

---

## Certificates vs SSH Keys

### SSH Keys

- Used mainly for remote login.
- Public key is manually added to the server.
- Trust is created manually.

### Certificates

- Used mainly on the Internet.
- Public key is inside the certificate.
- Trust is provided by a Certificate Authority (CA).

---

## Important Notes

✅ Certificate contains the Public Key.

❌ Certificate never contains the Private Key.

✅ Certificates verify identity.

✅ HTTPS uses Certificates for authentication.

---

# Interview Questions

### What is Authentication?

Authentication is the process of verifying the identity of a user, device, or server before granting access.

---

### What is Password Authentication?

A method of verifying identity using a username and password.

---

### What is a Certificate?

A digital identity card that binds a public key to its owner.

---

### Does a Certificate contain the Private Key?

No.

Only the Public Key.

---

### Why are Certificates required?

To verify that a public key belongs to its claimed owner.

---

### Who issues Certificates?

Certificate Authorities (CA).

---

# Memory Hook

```
Authentication

├── Password
│      ↓
│   Know Password
│
├── SSH Keys
│      ↓
│   Own Private Key
│
└── Certificate
       ↓
Verify Public Key Owner
```
