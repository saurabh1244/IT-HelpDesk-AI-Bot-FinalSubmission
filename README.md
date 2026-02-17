# IT Help Desk Voice Bot 🤖

A full-stack voice AI assistant designed to modernize IT support. The bot handles the entire ticket lifecycle—greeting the caller, identifying issues, collecting details, enforcing business rules, and sending email confirmations—through a natural voice conversation.

---

## 🔗 Project Links

- **Live Interface:** [voicebot.xiorabh.com](https://voicebot.xiorabh.com)
- **Video Demo:** [Insert Your Loom Video Link Here]
- **Frontend Repository:** [Help Desk Voice Bot Frontend](https://github.com/saurabh1244/Help_Desk_Voice_Bot_Frontend.git)
- **Backend Repository:** [Help Desk Voice Bot Backend](https://github.com/saurabh1244/Help_Desk_Voice_Bot_Assignment.git)

---

## 🛠️ Tech Stack & Architecture

| Component | Technology | Role |
|:---|:---|:---|
| **Voice AI** | Vapi | Speech-to-Text → LLM → Text-to-Speech pipeline |
| **Frontend** | React, TypeScript, Tailwind | Real-time dashboard with live activity feed |
| **Backend** | Node.js, Express | Business logic, tool handling, and validation |
| **Database** | Prisma ORM, SQLite | Relational data storage with type safety |
| **Email** | Brevo (SMTP) | Transactional email delivery |

---

## 🗄️ Database Design & Best Practices

I prioritized **data integrity** over flexibility. Unlike NoSQL solutions, I used a relational schema with Prisma to enforce strict types, ensuring that partial or invalid tickets are never created.

### Schema Highlights

```prisma
model Ticket {
  id        Int      @id @default(autoincrement())
  name      String
  email     String
  phone     String?
  address   String?
  issue     String   // Normalized to 4 specific categories
  price     Int      // Mapped server-side (Not LLM generated)
  createdAt DateTime @default(now())
}
```

### Key Design Decisions

- **Server-Side Price Mapping:** The price is never taken from voice input. It is determined by backend logic based on the issue category, preventing LLM hallucinations of discounts or incorrect fees.
- **Atomic Transactions:** Ticket creation and updates are separate, atomic operations.
- **Type Safety:** Strict typing on `Int` for IDs/Prices and `String` for contact info prevents format errors.

---

## 🧠 Edge Cases & Implementation Strategy

Relying solely on an LLM for business processes is error-prone. I implemented specific programmatic logic to handle these failure points:

### 1. Mid-Call Corrections (State Management)

**Scenario:** A user provides a phone number but immediately says, "Wait, actually use 9876..."

**Handling:** I implemented a specific `update_ticket` tool. If the user corrects themselves before the call ends, the bot detects the intent and updates only that specific field in the database without restarting the flow.

### 2. Price Integrity (Business Rule Enforcement)

**Scenario:** The LLM might accidentally quote a random price or agree to a user's haggling.

**Handling:** The backend strictly maps the issue to the `ISSUE_PRICE_MAP` constant. Even if the bot says "$15" for a Wi-Fi issue, the database will store the correct business price ($20).

### 3. System Resilience (External Failures)

**Scenario:** The email provider (Brevo) might be down or hit rate limits.

**Handling:** The email dispatch logic is wrapped in independent try-catch blocks. If the email service fails, the ticket is still safely saved in the database, ensuring no customer request is lost.

### 4. Unsupported Inputs

**Scenario:** A user complains about an issue not in the supported list (e.g., "The coffee machine is broken").

**Handling:** The backend validates the issue against the allowed list. If it doesn't match, it returns a structured error, prompting the bot to politely inform the user that it can only help with IT-related tasks.

---

## 📋 Business Rules (Fixed Fees)

The system enforces these exact service fees:

| Issue Category | Price |
|:---|:---|
| Wi-Fi Issues | $20 |
| Email/Password Reset | $15 |
| Slow Laptop (Performance) | $25 |
| Printer Fix | $10 |

---

## ⚙️ Local Setup

To run this project locally, configure the `.env` files as follows:

### Frontend Environment (`.env`)

```env
VITE_VAPI_PUBLIC_KEY=your_public_key
VITE_VAPI_ASSISTANT_ID=your_assistant_id
```

### Backend Environment (`.env`)

```env
PORT=5000
DATABASE_URL="file:./dev.db"
BREVO_API_KEY=your_brevo_api_key
SENDER_EMAIL=your_verified_sender_email
```

---

## 👤 Author

**Saurabh Chandra**

- **Portfolio:** [xiorabh.com](https://xiorabh.com)
- **LinkedIn:** [Saurabh Chandra](https://linkedin.com/in/saurabh-chandra)
- **Email:** saurabhchandra1244@gmail.com
