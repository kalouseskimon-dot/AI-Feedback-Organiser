# **AI Customer's Feedback Organiser**

An automated n8n workflow designed to ingest customer feedback, analyze and classify it using Google Gemini AI models, render formatted alert emails, log records into Supabase, and automatically generate draft response emails via Gmail.

---

## 🚀 **Architectural Overview**
This pipeline operates through a multi‑stage processing model:

1. **Ingestion**  
   Triggers when a response is submitted via **Typeform** (`Typeform Trigger`).

2. **Field Extraction & Normalization**  
   Extracts key data fields (e.g., `raw_content`, `sender_email`) from the Typeform payload and passes them downstream through a passthrough node (`Edit Fields1` -> `No Operation`).

3. **LLM Classification**  
   Processes the feedback using an **n8n AI Agent** backed by **Google Gemini** language models (`2.5 Flash Lite` / `3.1 Flash Lite`). The agent categorizes feedback and extracts structured metrics based on system instructions:
   - **Category**: `bug`, `feature_request`, or `general`
   - **Urgency**: `1` to `5`
   - **Summary**: 10-word core point summary
   - **Sentiment**: `Positive`, `Neutral`, or `Negative`

4. **JSON Structuring**  
   Parses raw text outputs from the primary AI agent using regular expressions (`JSON formatter`) to output uniform JavaScript objects containing clean values for category, urgency rating, summary, and sentiment.

5. **HTML Formatting & Dispatch**  
   - **HTML Beautifier**: Evaluates the severity of the feedback. Critical bugs (Category: `bug` with Urgency $\ge$ `4`) trigger special high-priority styling (red accent color, critical alert headers).
   - **Email Converter**: Converts the alert payload into a clean HTML layout.
   - **Info Message**: Sends the formatted alert email directly to the designated support inbox using **Gmail**.

6. **Database Logging & Draft Generation**  
   - **Supabase Integration**: Inserts the parsed feedback entry directly into the `feedbacks` table (`Create a row`).
   - **AI Auto-Response Generation**: Passes context to a second **AI Agent** (`AI Agent1`) powered by **Google Gemini Chat Models** to draft a contextual response email.
   - **Gmail Draft Creation**: Creates a pending message draft in Gmail (`Create a draft`) thanking the customer.
   - **Database Update**: Updates the existing record in **Supabase** (`Update a row`) to signal completed workflow execution.

---

## 🛠 **Prerequisites**
- **n8n Instance** (Self‑hosted or Cloud)
- **Google Gemini API Key** (`Google Gemini(PaLM) Api`)
- **Typeform Account & API Key**
- **Gmail OAuth2 Credentials**
- **Supabase Account & Credentials**

---

## 📥 **Installation**
1. **Import Workflow**: Import the `AI Customer's Feedback Organiser` JSON file into your n8n workspace.
2. **Setup Credentials**:
   - Link your **Typeform API** account in the `Typeform Trigger` node.
   - Set up **Google Gemini (PaLM) API** credentials for the Gemini chat model nodes.
   - Authenticate **Gmail OAuth2** credentials for sending alerts (`Info Message`) and drafting replies (`Create a draft`).
   - Configure **Supabase API** credentials for database operations (`Create a row`, `Update a row`).
3. **Configure Nodes**:
   - Set your specific `formId` inside the `Typeform Trigger` node.
   - Update the recipient email address inside the `Info Message` Gmail node.
   - Update the target Supabase table name or schema in the Supabase nodes if necessary.
4. **Activate**: Toggle the workflow switch to **Active**.

---

## ⚖️ **License**
Distributed under the **MIT License**.
