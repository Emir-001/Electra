# 🚀 Electra — AI-Assisted Financial Risk Simulator

**A multi-agent LLM system that analyses personal finances using live macroeconomic data (RAG).**

👉 **[Live Demo](https://ai-assisted-financial-risk-simulator-44fben3bq-emir-hackathon.vercel.app)** *(optimised for desktop; mobile support is planned)*

Electra analyses a user's income, expenses, debt structure and savings goals. Instead of applying static rules, it combines official macroeconomic data from Türkiye and the world with Google Gemini's reasoning to produce personalised risk reports, 12-month savings projections and prioritised action plans.

---

## 🌟 Key Features

### 1. Multi-Agent AI Orchestration 🧠
Instead of asking a single model, the app runs **4 specialised AI agents** in parallel and merges their output into one decision:
* **Macro Agent:** analyses how current inflation, Central Bank of the Republic of Türkiye (CBRT) policy rates and currency risk affect the user's savings and debt.
* **Credit Agent:** evaluates debt-to-income ratio (DTI), emergency fund adequacy (3–6 month standard) and financial sustainability.
* **Sector Agent:** lists risks and opportunities across real estate, FX, commodities and the labour market for the user's profile.
* **Supervisor Agent:** synthesises the three reports into a **Financial Health Score (0–100)**, a **12-month savings projection** and a **prioritised action plan**.

### 2. Live RAG (Retrieval-Augmented Generation) Pipeline 📡
No file uploads needed — the system fetches live data from official sources in the background:
* **CBRT:** daily XML exchange-rate bulletin (USD, EUR, GBP, JPY).
* **World Bank API:** Türkiye CPI inflation (last 3 years) and GDP growth (last 2 years).
* **St. Louis Fed (FRED):** current and historical USD/TRY trends.
* **OECD:** quarterly growth and monetary policy context for Türkiye.
* *Optimisation:* all data is served through a **1-hour in-memory cache** to stay within API quotas and keep responses fast.

### 3. Gemini Model Cascade (Fault Tolerance) 🛡️
To handle rate limits (`429` / `RESOURCE_EXHAUSTED`) and model availability errors, a **model cascade** automatically falls back to the next model without interrupting the user:
1. `gemini-3.1-flash-lite`
2. `gemini-2.5-flash`
3. `gemini-2.0-flash`
4. `gemini-flash-latest`
5. `gemini-flash-lite-latest`
6. `gemini-3-flash-preview`

### 4. PDF Report Export 📄
A multi-page A4 report generated entirely in the browser (`jspdf`, `html-to-image`):
* Financial profile: income, expenses, savings, debt, DTI and emergency fund metrics
* Colour-coded Financial Health Score card
* Action plans tagged `Urgent`, `Important` and `Long-term`
* Detailed findings from each agent and a sector risk matrix by severity

### 5. UI/UX and Micro-Animations 🎨
* **Interactive market background:** an HTML5 Canvas animation with live candlestick charts, a 7-day SMA curve, dynamic support/resistance levels and price pulse effects.
* **Proportional spending slider:** changing total spending rescales budget sub-categories (rent, bills, food…) while keeping their ratios.
* Dark/light theme toggle, text reveal effects and Framer Motion transitions.

---

## 💻 Tech Stack

* **Frontend:** Next.js (App Router, React 19), Tailwind CSS, Framer Motion, Recharts, Lucide React
* **Design:** Radix UI, `@wrksz/themes`, Magic UI (`DiaTextReveal`)
* **AI & RAG:** `@google/generative-ai` (Gemini SDK), CBRT & World Bank API integrations
* **Data layer:** Drizzle ORM, PostgreSQL
* **Reporting:** jsPDF, html2canvas, html-to-image

---

## 🛠️ Getting Started

### Prerequisites
* Node.js v18+
* PostgreSQL database
* Google Gemini API key

### Steps

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Set environment variables (`.env.local`):**
   ```env
   GEMINI_API_KEY=your_gemini_api_key
   DATABASE_URL=postgresql://user:password@host:port/database
   ```

3. **Start the dev server:**
   ```bash
   npm run dev
   ```

4. Open [http://localhost:3000](http://localhost:3000)
