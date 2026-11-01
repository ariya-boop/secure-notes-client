# CipherVault | Zero-Knowledge Encrypted Notes Client

A modern, client-side, zero-knowledge web application that provides end-to-end encryption for sensitive data using the native browser **Web Crypto API**.

Designed to interface with the [secure-notes-api](https://github.com/ariya-boop/secure-notes-api) backend or operate completely standalone in local storage.

---

## 1. Zero-Knowledge Architecture

In zero-knowledge architecture, the server never receives, stores, or processes unencrypted plaintext or encryption keys. Even if the backend database is compromised, all data remains cryptographically undecipherable.

```
+-------------------------------------------------------------+
|                      Client Browser                         |
|                                                             |
|  [ Master Passphrase ]                                      |
|          |                                                  |
|          v (PBKDF2, SHA-256, 100,000 iterations + Salt)     |
|  [ 256-bit AES-GCM Key ]                                    |
|          |                                                  |
|          +----------> [ Encrypt Plaintext + IV ]            |
|                              |                              |
+------------------------------|------------------------------+
                               v (Only Ciphertext + IV sent)
                 +---------------------------+
                 |    Secure Notes Backend   |
                 |      (Zero-Knowledge)     |
                 +---------------------------+
```

---

## 2. Cryptographic Specifications

- **Cipher**: AES-256-GCM (Galois/Counter Mode) authenticated encryption.
- **Key Derivation Function (KDF)**: PBKDF2 with SHA-256 and **100,000 iterations**.
- **Initialization Vector (IV)**: 12-byte cryptographically secure pseudorandom numbers generated via `crypto.getRandomValues()` for every encryption operation.
- **Key Retention Policy**: Derived cryptographic keys exist solely in transient memory; keys and plaintext are wiped from memory on vault lock or session termination.

---

## 3. Features

- **End-to-End Encryption**: Zero unencrypted data leaves the browser.
- **Instant Search & Decryption**: In-memory decryption allows fast searching across encrypted note headers and bodies.
- **Visual Cryptographic Feedback**: Displays real-time IV, Salt, and Ciphertext previews for security auditing.
- **Zero External Dependencies**: Pure vanilla HTML5, CSS3, and modern ES6 JavaScript utilizing native W3C Web Cryptography APIs.
- **Responsive Dual-Pane UI**: Dark-mode terminal inspired interface with responsive sidebar and real-time encryption indicators.

---

## 4. Getting Started

Simply open `index.html` in any modern web browser:
```bash
# Clone the repository
git clone https://github.com/ariya-boop/secure-notes-client.git
cd secure-notes-client

# Open in browser (Windows)
start index.html
```

Or access the live deployment directly via GitHub Pages:
[https://ariya-boop.github.io](https://ariya-boop.github.io)
