# SSH Keys Commands

## Generate SSH Key Pair

```bash
ssh-keygen
```

Creates:

```
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

---

## View Public Key

```bash
cat ~/.ssh/id_ed25519.pub
```

---

## Copy Public Key to Remote Machine

```bash
ssh-copy-id username@remote-ip
```

Example:

```bash
ssh-copy-id ubuntu@192.168.1.20
```

---

## Login Using SSH Key

```bash
ssh username@remote-ip
```

Example:

```bash
ssh ubuntu@192.168.1.20
```

---

## Create .ssh Directory (Manual Setup)

```bash
mkdir -p ~/.ssh
```

---

## Open authorized_keys

```bash
nano ~/.ssh/authorized_keys
```

Paste your public key into this file.

---

## List SSH Files

```bash
ls -la ~/.ssh
```

---

## View Authorized Public Keys

```bash
cat ~/.ssh/authorized_keys
```

---

## Remove a Public Key

Edit the file:

```bash
nano ~/.ssh/authorized_keys
```

Delete the unwanted public key.

---

# Common File Locations

Local Machine

```
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

Remote Machine

```
~/.ssh/authorized_keys
```

---

# Interview Questions

### Which key is copied to the server?

Public Key

---

### Which key stays on your computer?

Private Key

---

### Can the Private Key be shared?

No.

---

### Where are trusted public keys stored?

```
~/.ssh/authorized_keys
```

---

### What command generates SSH Keys?

```bash
ssh-keygen
```

---

### What command copies the Public Key to the server?

```bash
ssh-copy-id username@remote-ip
```
