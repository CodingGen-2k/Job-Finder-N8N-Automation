# 🔎 AI Job Finder Automation (n8n)

This project is an **n8n-based AI job finder automation**.  
It reads a resume, builds LinkedIn job searches, extracts job details, scores them using AI, stores results in Google Sheets, and sends job alerts to Telegram.

---

## ⚙️ Requirements

Before starting, you must have:

- n8n (local / Docker / cloud)
- Telegram account
- Google account
- OpenRouter (or OpenAI-compatible) API key
- Google Drive & Google Sheets access

If any of these are missing, the workflow will fail.

---

## 📥 Import Workflow into n8n (Copy-Paste JSON)

1. Open **n8n Dashboard**
2. Click **New Workflow**
3. Click the **three dots (⋮)** in the top-right corner
4. Select **Import from clipboard**
5. Open `Job Finder.json` in a text editor
6. **Copy the entire JSON**
7. Paste it into n8n and click **Import**
8. Save the workflow

If you paste incomplete JSON, the workflow will break. Copy everything.

---

## 🤖 Telegram Setup (Trigger + Messages)

### 1. Create Telegram Bot
- Open Telegram → search **@BotFather**
- Run:
- /start
- /newbot

- - Copy the **Bot Token**

### 2. Add Telegram Credentials in n8n
- Go to **Credentials**
- Create **Telegram API**
- Paste the Bot Token
- Read from oficial site "https://docs.n8n.io/integrations/builtin/credentials/telegram/?utm_source=n8n_app&utm_medium=credential_settings&utm_campaign=create_new_credentials_modal"

### 3. Telegram Trigger Node
- Open **Telegram Trigger**
- Select your Telegram credentials
- Update types: `message`
- Save node

### 4. Get Chat ID
- Send any message to your bot
- Check execution data → copy `chat.id`
- Paste it inside **Send a text message** node

---

## 📄 Google Drive Setup (Resume)

1. Upload your resume PDF to Google Drive
2. Right-click → **Get link**
3. Set access to **Anyone with the link**
4. Copy file URL
5. Paste it into **Download Resume** node (`File ID → URL mode`)
6. Official setup guide page link "https://docs.n8n.io/integrations/builtin/credentials/google/oauth-generic/#scopes"

---

## 📊 Google Sheets Setup (Database)

### 1. Create Google Sheet
Create a sheet with **two tabs**:

#### Sheet 1: `Data`
Used for job search parameters  
Columns:
- Keyword
- Location
- Experience Level
- Remote
- Job Type
- Easy Apply

#### Sheet 2: `Result`
Used for final job results  
Columns:
- Title
- Company
- Location
- Link
- Description
- Score
- Cover Letter

---

### 2. Google Sheets Credentials
- Go to **Credentials**
- Create **Google Sheets OAuth2**
- Sign in and allow access
- Read from this offical page "https://docs.n8n.io/integrations/builtin/credentials/google/oauth-generic/#scopes"

### 3. Update Sheet IDs
Update these nodes with your Sheet ID:
- **Job Search Parameters**
- **Append or update Data into sheet**

---

## 🧠 AI Model Setup (OpenRouter)

1. Create account on OpenRouter
2. Copy API Key
3. In n8n:
 - Create **OpenRouter API** credentials
 - Paste API key
4. Assign credentials to **OpenRouter Chat Model** node
   BONUS : You can get free llm models apis from OpenRouter Official website

---

## ▶️ How to Start the Workflow

### Option 1: Telegram (Manual)
- Send `start` to your Telegram bot
- Workflow starts immediately

### Option 2: Schedule (Automatic)
- Open **Schedule Trigger**
- Set interval (hourly / daily)
- Activate workflow

---

## 📤 Output

- Jobs are scored using AI
- High-score jobs are:
- Stored in Google Sheets
- Sent to Telegram with job details and cover letter

---

## 🛑 Notes

- LinkedIn HTML structure may change
- Scraping logic can break anytime
- This project is for automation learning and demo purposes

---

## 📌 Files

- `Job Finder.json` → n8n workflow (copy-paste import)
- `README.md` → setup guide

---

## 👤 Author

Built by **Hamza**  
Focus: AI automation, n8n workflows, real-world integrations
