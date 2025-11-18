# Configurare SMTP Gmail pentru Formularul de Contact IrisAI

Acest ghid te va ajuta să configurezi Gmail SMTP pentru formularul de contact de pe site-ul IrisAI.

---

## Pasul 1: Obține App Password de la Gmail

Pentru Gmail Workspace, trebuie să creezi un **App Password** (nu parola contului):

1. **Mergi la Google Account**: [https://myaccount.google.com](https://myaccount.google.com)
2. **Security** → **2-Step Verification** (trebuie să fie activată)
3. **App passwords** → **Select app** → **Mail**
4. **Select device** → **Other (Custom name)** → Scrie "IrisAI Contact Form"
5. **Generate** → **Copiază parola generată** (16 caractere, fără spații)

---

## Pasul 2: Adaugă Environment Variables în Vercel

1. **Accesează Vercel Dashboard**: [https://vercel.com/dashboard](https://vercel.com/dashboard)
2. **Selectează Proiectul**: Alege proiectul `iris-landing` (sau numele proiectului tău)
3. **Navighează la Environment Variables**:
   - Click pe **"Settings"** (Setări)
   - Selectează **"Environment Variables"** (Variabile de Mediu)
4. **Adaugă următoarele variabile**:

   | Name | Value | Environment |
   |------|-------|-------------|
   | `SMTP_USER` | `contact@irisai.ro` | Production, Preview, Development |
   | `SMTP_PASS` | `[App Password generat]` | Production, Preview, Development |

   **Important**: 
   - Pentru `SMTP_PASS`, folosește **App Password** (nu parola contului)
   - Bifează toate environment-urile (Production, Preview, Development)
   - Click pe **"Add"** pentru fiecare variabilă

---

## Pasul 3: Instalează Dependențele

Vercel va instala automat `nodemailer` din `package.json` când face deploy.

Dacă vrei să testezi local, rulează:
```bash
cd iris-standalone
npm install
```

---

## Pasul 4: Deploy pe Vercel

După ce ai adăugat Environment Variables, Vercel va face automat redeploy. Dacă nu, poți declanșa un deploy manual din dashboard-ul Vercel sau prin `git push`.

---

## Pasul 5: Testează Formularul

1. Mergi la https://irisai.ro/contact
2. Completează formularul și trimite-l
3. Verifică email-ul la `contact@irisai.ro` - ar trebui să primești mesajul

---

## Configurare SMTP

- **Host**: `smtp.gmail.com`
- **Port**: `587` (TLS/STARTTLS)
- **User**: `contact@irisai.ro`
- **Password**: App Password generat de la Google
- **From**: `contact@irisai.ro`
- **To**: `contact@irisai.ro`

---

## Troubleshooting

### Eroare: "Invalid login"
- Verifică că folosești **App Password**, nu parola contului
- Verifică că 2-Step Verification este activată

### Eroare: "Connection timeout"
- Verifică că portul este `587` (nu `465`)
- Verifică că `secure: false` în cod (pentru port 587)

### Email-urile nu ajung
- Verifică Spam/Junk folder
- Verifică că `SMTP_USER` și `SMTP_PASS` sunt setate corect în Vercel
- Verifică Vercel Logs pentru erori

---

## Notă Importantă

**NU** pune niciodată App Password în cod! Folosește întotdeauna Environment Variables în Vercel.

