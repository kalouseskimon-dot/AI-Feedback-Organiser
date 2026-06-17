🎛️ # AI Customer Feedback Organiser

Automatically capture, classify, and escalate customer feedback from multiple channels using AI‑powered analysis and beautifully formatted email alerts.

✨ Features
📥 Multi‑source feedback intake (Gmail, Typeform, Webhooks)

🧹 Intelligent noise filtering

🧠 AI‑powered categorization using Google Gemini

🏷️ Auto‑extracted metadata (email, content, urgency, sentiment)

🚨 Critical‑bug escalation logic

🎨 HTML‑formatted alert emails

📊 Google Sheets logging

⚡ Fully automated with n8n

🛡️ Error‑handling workflow with email notifications

🏗️ Workflow Architecture
Gmail / Typeform / Webhook
  ↓
Noise Filtering
  ↓
Field Extraction
  ↓
AI Categorization Agent
  ↓
JSON Parsing
  ↓
HTML Beautifier
  ↓
Email Renderer
  ↓
Gmail Alert
  ↓
Google Sheets Logging

🚀 How It Works
1. Multi‑Channel Feedback Intake
The workflow listens for new feedback from:

Gmail messages

Typeform submissions

Custom webhook events

2. Noise Filtering
Emails containing words like unsubscribe, invoice, receipt, or shipping are removed.
Only messages containing feedback‑related terms (e.g., bug, feature, problem, idea) continue.

3. Field Extraction
Depending on the source, the workflow extracts:

Raw message content

Sender email

Subject line

Timestamp

4. AI Feedback Analysis
A Google Gemini agent classifies each message into:

Category (bug, feature_request, general)

Urgency (1–5)

Sentiment (Positive, Neutral, Negative)

10‑word summary

Sender email

5. JSON Formatting
Regex parsing converts the AI output into clean JSON fields.

6. HTML Beautification
The workflow generates a polished HTML email with:

Dynamic color coding

Critical‑bug alert banners

Summary section

Quick‑action button

7. Automated Delivery
The formatted alert is sent to your inbox via Gmail.

8. Google Sheets Logging
Each feedback entry is appended or updated in a Google Sheet for tracking and analytics.

9. Error Workflow
If anything fails, a separate workflow triggers an email notifying you of the issue.

📚 Example Output
Each alert email includes:

Feedback Overview
Category: BUG

Urgency: 5

Sentiment: Negative

Email: user@example.com

Summary
A concise 10‑word description of the issue.

Critical Alert Banner
Displayed when:

Category = bug

Urgency ≥ 4

Quick Action Button
View & Resolve Immediately (for critical bugs)

View in Database (for all others)

🛠️ Technology Stack
Technology	Purpose
n8n	Workflow automation
Google Gemini	AI classification
Gmail	Email alerts
Google Sheets	Feedback storage
HTML/CSS	Email formatting


🎯 Benefits
For Support Teams
Faster triage

Automatic prioritization

Clear summaries for quick action

For Product Teams
Structured feedback insights

Easy tracking in Google Sheets

For Founders
Automated customer‑listening system

Instant alerts for critical issues

📈 Future Enhancements
Auto‑reply to customers

Slack / Teams notifications

Multi‑language sentiment analysis

Dashboard for analytics

Duplicate‑feedback detection

🔥 Production Architecture
Gmail / Typeform / Webhook
 ↓
Noise Filter
 ↓
AI Categorizer
 ↓
HTML Renderer
 ↓
Gmail
 ↓
Google Sheets

📄 License
MIT License

Built with ❤️ using n8n, Google Gemini, Gmail, and automated HTML rendering.
