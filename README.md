# 🤖 IT Help Desk Voice Bot – Take-Home Assignment

Welcome to the **Next-Gen AI Support System**. This project is a full-stack voice-controlled assistant designed to modernize IT support by automating ticket creation through natural voice conversations.



---

### 🔗 Project Ecosystem
* **Live Dashboard:** [voicebot.xiorabh.com](https://voicebot.xiorabh.com)
* **Video Demo:** [Insert Your Loom/Video Link Here]
* **Frontend Repository:** [GitHub Link](https://github.com/saurabh1244/Help_Desk_Voice_Bot_Frontend.git)
* **Backend Repository:** [GitHub Link](https://github.com/saurabh1244/Help_Desk_Voice_Bot_Assignment.git)

---

### 🛠️ Tech Stack & Architecture

| Layer | Technology |
| :--- | :--- |
| **Voice Interface** | Vapi (STT → LLM → TTS Pipeline) |
| **Frontend** | React (Vite), TypeScript, Tailwind CSS, Framer Motion |
| **Backend** | Node.js, Express, TypeScript |
| **Database** | Prisma ORM, SQLite (Deployed on Render) |
| **Automation** | Brevo (SMTP Email Integration) |
| **Icons** | Lucide React |



---

### 🚀 Key Features & Edge Cases Handled

LLMs alone can fail in complex business scenarios. This project implements robust logic to handle:

* **Real-time Data Correction:** Using the `update_ticket` tool, users can modify details (like phone or address) mid-conversation if they make a mistake.
* **Dynamic Server-Side Pricing:** Service fees are mapped on the backend (`ISSUE_PRICE_MAP`) ensuring 100% accuracy with business rules ($20 for Wi-Fi, $25 for Slow Laptop, etc.).
* **Live Activity Feed:** The frontend listens to Vapi events. As soon as a ticket is created/updated, the dashboard refreshes automatically without a page reload.
* **Graceful Interruption:** The bot handles user interruptions naturally, allowing a fluid "human-like" conversation flow.

---

### 📋 Business Rules (Golden Path)
The bot is programmed to follow these specific IT support scenarios:
- **Wi-Fi Issues:** $20
- **Email/Password Reset:** $15
- **Slow Performance (CPU Change):** $25
- **Printer Problems:** $10

---

### 👤 Developer Profile
**Saurabh Chandra**
* **Portfolio:** [xiorabh.com](https://xiorabh.com)
* **LinkedIn:** [Saurabh Chandra](https://www.linkedin.com/in/saurabh-chandra-454600268/)
* **GitHub:** [@saurabh1244](https://github.com/saurabh1244)
* **Email:** Saurabhchandra1244@gmail.com

---

### ⚙️ Local Setup
1. Clone the master repo.
2. Install dependencies in both folders: `npm install`.
3. Set up `.env` with `VITE_VAPI_PUBLIC_KEY`, `VITE_VAPI_ASSISTANT_ID`, and `DATABASE_URL`.
4. Run `npx prisma migrate dev` for the database.
5. Use `npm run dev` to start both local servers.
