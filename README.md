# **AI Customer Feedback Organiser**

An automated n8n workflow designed to ingest customer feedback from multiple channels, classify it using AI, filter noise, and deliver structured HTML alerts while logging all insights into Google Sheets.

---

## 🚀 **Architectural Overview**
This pipeline operates through a multi‑stage processing model:

1. **Ingestion**  
   Collects feedback from **Gmail**, **Typeform**, and **custom Webhooks**, ensuring all customer touchpoints are captured.

2. **Noise Filtering**  
   A JavaScript filter removes irrelevant emails such as unsubscribe notices, receipts, and automated system messages, preserving only genuine feedback.

3. **Field Extraction**  
   Normalizes raw content, sender email, subject line, and timestamps across all input sources for consistent downstream processing.

4. **LLM Classification**  
   Uses **Google Gemini Flash models** via LangChain to determine:  
   - Category (bug, feature_request, general)  
   - Urgency (1–5)  
   - Sentiment  
   - 10‑word summary  
   - Sender email  

5. **JSON Structuring**  
   Regex‑based parsing converts the AI output into clean, structured JSON fields suitable for storage and rendering.

6. **HTML Rendering**  
   A custom HTML generator produces branded, color‑coded alert emails with critical‑bug escalation logic and action buttons.

7. **Dispatch**  
   Sends formatted alerts via **Gmail** and logs all entries into **Google Sheets** for long‑term tracking and analytics.

8. **Error Handling**  
   A dedicated error workflow triggers an email notification whenever execution fails, ensuring operational reliability.

---

## 🛠 **Prerequisites**
- **n8n Instance** (self‑hosted or Cloud)  
- **Google Gemini API Key** (for AI classification)  
- **Gmail OAuth2 Credentials**  
- **Google Sheets OAuth2 Credentials**  
- Optional: **Webhook endpoint** or **Typeform form**

---

## 📥 **Installation**
1. Import the workflow JSON into your n8n dashboard.  
2. Configure your **Google Gemini(PaLM) Api** credentials in the AI Agent node.  
3. Connect your **Gmail OAuth2** credentials for message retrieval and alert delivery.  
4. Link your **Google Sheets** credentials for logging.  
5. (Optional) Replace webhook paths or Typeform form IDs with your own.

---

## ⚖️ **License**
Distributed under the **MIT License**.
