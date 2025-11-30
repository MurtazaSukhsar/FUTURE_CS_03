# Secure Share 🔐
🚀 Live Demo: **https://secure-file-sharing-fl6d.onrender.com**

Secure Share is a Flask web app for **encrypted file sharing**.  
Users can sign up, log in, upload files, and generate share links with optional passwords – all using a **single pre-configured Supabase project**, so you don’t need to set up your own backend.


> To run this project locally you only need Python and the dependencies listed in `requirements.txt`.

---

## 🚀 Features

- 🔑 Email/password authentication using Supabase Auth  
- 🔐 AES-encrypted file uploads — only encrypted `.enc` files are stored  
- 🧾 User dashboard to manage personal files  
  - View only your own uploads  
  - Download (decrypted on the fly)  
  - Delete files  
- 🔗 Secure share links  
  - Random share token per file  
  - Optional password protected downloads  
- 🗑 Temporary decrypted files stored in `temp/` and auto-removed after use

---

## 🛠 Tech Stack

| Component | Technology |
|----------|------------|
| Language | Python 3.10+ |
| Backend  | Flask |
| Auth / Storage / DB | Supabase |
| Encryption | PyCryptodome (AES) |
| Templating | Jinja2 + Bootstrap UI |

---

## 📌 Requirements

- Python **3.10 or newer**
- (Optional) Git to clone the project

You **do not need**:

- A Supabase account  
- Any external configuration  

Supabase keys + storage are already wired into the project.

---

## ⚙️ Installation & Local Run

### 1. Clone the repository

```bash
git clone https://github.com/MurtazaSukhsar/FUTURE_CS_03
cd secure-file-sharing
```

Or download ZIP and extract manually.

### 2. Create a virtual environment (recommended)

```bash
python -m venv venv
```

Activate:

| OS | Command |
|----|---------|
| Windows | `venv\Scripts\activate` |
| macOS/Linux | `source venv/bin/activate` |

### 3. Ensure `requirements.txt` contains:

```
flask
gunicorn
supabase
pycryptodome
```

### 4. Install required packages

```bash
pip install -r requirements.txt
```

### 5. Run the server

```bash
python app.py
```

### 6. Open in browser

```
http://127.0.0.1:5000
```

Create an account → Upload files → Create share links → Download securely.

---

## 🔍 How It Works

### Upload Flow
1. File saved temporarily on server  
2. Encrypted using AES (PyCryptodome)  
3. Uploaded to Supabase Storage as `.enc`  
4. Metadata stored in Supabase DB (owner, token, optional password)

### Download Flow
1. Encrypted blob fetched from storage  
2. Decrypted in RAM → temporary file generated  
3. File served to user  
4. Temp file deleted immediately

---

## 🔒 Security Notes

- Replace demo `AES_KEY` + Flask `SECRET_KEY` before serious use  
- Use environment variables for secrets  
- Supabase RLS ensures users only access their own data  
- Recommended for learning & light personal use, not production-grade yet

---
