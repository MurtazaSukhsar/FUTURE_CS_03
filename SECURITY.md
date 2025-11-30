# Security Overview

Secure Share is designed as a learning project for encrypted file sharing.  
It uses **AES encryption**, **Supabase Auth + Row Level Security (RLS)**, and standard Flask security practices to protect user data.

---

## 1. Data Protection

### 🔐 Encryption at Rest
- Files are encrypted using **AES (PyCryptodome)** in EAX mode before upload.
- Only encrypted `.enc` blobs are stored — plaintext files never remain in storage.

### 🔒 Encryption in Transit
- All communication between the app and Supabase occurs over **HTTPS / TLS**.
- File transfers, authentication tokens, and metadata are protected during transit.

### 🗑 Temporary Files
- Plaintext decrypted files exist only inside the `temp/` directory during upload/download.
- Temporary files are deleted automatically after being served.

---

## 2. Authentication & Authorization

### 🔑 Authentication
- Handled by **Supabase Auth** (Email + Password).
- The server never stores raw plaintext passwords.

### 🧾 Row‑Level Isolation
- A Supabase table stores metadata per file along with owner ID.
- **RLS policies** ensure users only read/modify files belonging to their own `auth.uid()`.

### 🔐 Session Handling
- Flask uses signed cookies for session tracking.
- Production deployments should enable:
  ```
  SESSION_COOKIE_SECURE = True
  SESSION_COOKIE_HTTPONLY = True
  SESSION_COOKIE_SAMESITE = 'Lax'
  ```

---

## 3. Key Management

### AES Encryption Key
- Current key is static for demonstration.
- For secure deployments:
  - Store the key in environment variables.
  - Rotate keys periodically and never commit secrets to Git.

### Supabase Keys
- Only **anon key** is exposed on the server — service keys are never used here.
- Supabase secrets should also be environment-based.

---

## 4. Application Hardening Recommendations

To move beyond educational use:

| Area | Recommended Improvement |
|------|--------------------------|
| Web Transport | Force HTTPS |
| Forms | Add CSRF protection |
| Secrets | Move to .env or secret manager |
| Storage Policies | Enforce RLS + user-bound access |
| Logging | Track failed logins + access attempts |
| Package Security | Keep dependencies updated |

---

## 5. Limitations

- Intended for **learning + light personal use**, not high‑security enterprise use.
- Does not include:
  - MFA / 2FA,
  - Encrypted audit logs,
  - Advanced key rotation workflows,
  - Enterprise‑grade monitoring or isolation layers.

Before handling sensitive production data, a full security review is strongly recommended.

---
