# SSH Keys Authentication

SSH Keys provide a secure way to log in to a remote machine **without typing the server's password every time**.

Instead of remembering passwords, SSH uses a **Public Key** and a **Private Key**.

---

# Key Pair

When you generate SSH keys, two files are created.

```
Private Key 🔒
Public Key 🌍
```

### Private Key

- Stays on your local machine.
- Never share it with anyone.
- Used to prove your identity.

### Public Key

- Can be shared safely.
- Stored on the remote server.
- Used by the server to verify your identity.

---

# One-Time Setup

## Step 1 - Generate SSH Keys

On your local machine:

```bash
ssh-keygen
```

This creates:

```
~/.ssh/

id_ed25519
id_ed25519.pub
```

or

```
id_rsa
id_rsa.pub
```

---

## Step 2 - Copy Public Key to Remote Machine

The easiest method:

```bash
ssh-copy-id username@remote-ip
```

Example:

```bash
ssh-copy-id ubuntu@192.168.1.20
```

This copies your public key to the remote machine.

---

## Manual Method

If you cannot use `ssh-copy-id`, copy the contents of:

```
~/.ssh/id_ed25519.pub
```

Then paste it into the remote machine:

```
~/.ssh/authorized_keys
```

If the `.ssh` folder doesn't exist, create it.

```
mkdir -p ~/.ssh
```

Then create or edit:

```
~/.ssh/authorized_keys
```

Paste your public key inside this file.

---

# Login Process

After the public key is registered:

```
ssh username@remote-ip
```

The server checks:

"Do I have this user's public key?"

↓

If YES

↓

Your local machine automatically proves that it owns the matching private key.

↓

Login Successful

No server password is required.

---

# Where is the Private Key Used?

The private key always stays on your local machine.

You never copy it to the server.

The SSH client automatically uses it during login.

You do not manually select it every time.

---

# Real-Life Example

Suppose your friend has an Ubuntu PC.

Initially:

```
ssh friend@192.168.1.50
```

The server asks:

```
Password:
```

You enter the password.

Login Successful.

---

Now your friend wants passwordless login.

He asks:

"Send me your public key."

You send:

```
id_ed25519.pub
```

He adds it to:

```
~/.ssh/authorized_keys
```

Now you simply run:

```
ssh friend@192.168.1.50
```

No password is required.

Because your public key is already registered.

---

# Company Server Example

Most companies use SSH Keys instead of passwords.

Developer

↓

Generates SSH Keys

↓

Sends Public Key to System Administrator

↓

Administrator adds it to:

```
~/.ssh/authorized_keys
```

Now only registered developers can log in.

If an employee leaves the company,

the administrator simply removes that public key.

No password needs to be changed.

---

# Cloud Example (AWS / Azure / GCP)

When creating a cloud server,

you are asked to choose an SSH Key Pair.

Cloud provider installs your public key on the server.

Later you log in using:

```bash
ssh ubuntu@public-ip
```

without entering the server password.

---

# Important Notes

✅ Public Key can be shared.

❌ Private Key must never be shared.

✅ Public Key is stored on the remote machine.

✅ Private Key always stays on your local machine.

---

# Authentication Flow

```
Local Machine                     Remote Machine

Private Key 🔒

Public Key 🌍
      │
      └──────────────► authorized_keys

Later...

ssh username@ip

        │
        ▼

Server checks authorized_keys

        │

If Public Key Found

        │

Local machine proves ownership of
the matching Private Key

        │

Login Successful
```

---

# Memory Hook

```
Private Key

↓

Keep Secret

↓

Stays on Your Computer

----------------------------

Public Key

↓

Share Freely

↓

Store on Remote Machine
```
