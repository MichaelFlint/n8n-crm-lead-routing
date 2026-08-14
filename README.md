# 🚀 Automated CRM Lead Routing & Scoring System (n8n + OpenAI + Airtable)

![n8n](https://img.shields.io/badge/n8n-FF6D5A?style=for-the-badge&logo=n8n&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)
![Airtable](https://img.shields.io/badge/Airtable-18BFFF?style=for-the-badge&logo=airtable&logoColor=white)

An automated system designed to capture, deduplicate, normalize, and prioritize leads (Lead Scoring) incoming from web forms directly into a CRM (Airtable).

---

## 🎯 Business Problem

Manual processing of contact form submissions causes response delays, creates duplicate records in the CRM, and results in missed opportunities to instantly act on high-value B2B prospects (*High-Priority leads*).

**The Solution:**
This workflow automates the entire intake pipeline in real-time:
1. Receives data via Webhook (Web Form submission).
2. Checks for existing records in Airtable by email address (Deduplication).
3. **If exists:** Updates the contact record and logs the new touchpoint.
4. **If new:** Passes data to OpenAI API for intent recognition, data normalization, and **Lead Scoring (0-100)**.
5. Saves the processed lead into the appropriate sales pipeline (High / Low Priority) inside Airtable CRM.

---

## 🏗️ Architecture & Data Flow
[ Webhook Trigger ]
│
▼
[ Airtable: Search Lead ]
│
┌────┴─────────────────────────┐
▼                              ▼
(Lead Exists?)               (New Lead)
│                              │
├─► TRUE: [Airtable Update]    └─► [OpenAI: JSON Schema Normalization & Scoring]
│                                                     │
└─────────────────────────────────────────────────────┴─► [Airtable Create Record]

## 🛠️ Tech Stack

* **Orchestration:** n8n (Webhook Node, IF / Switch Node, Airtable Node, Code Node)
* **AI Engine:** OpenAI API (`gpt-4o-mini`) using **Structured Outputs / JSON Schema**
* **Database / CRM:** Airtable API
* **Logic & Transformation:** JavaScript (`Code Node` in n8n)

---

## ✨ Key Features & Production Readiness

- **Zero Duplicates (Deduplication):** Prevents multiple entries for the same client by searching the CRM prior to record creation.
- **Strict Data Schemas:** Uses OpenAI Structured Outputs (JSON Schema) to guarantee reliable, predictable JSON responses without hallucinated keys.
- **Data Standardization:** Validates and cleans phone numbers, names, and company details before database insertion.
- **Intelligent Lead Scoring:** Automatically evaluates purchase intent based on AI analysis of the user's message context.

---

## ⚙️ How to Run / Setup

### Prerequisites
* A running instance of n8n (Cloud or Self-Hosted).
* An active OpenAI API key.
* An Airtable account with a base set up for Lead Management.

### Setup Steps
1. Download the `workflow.json` file from this repository.
2. In your n8n canvas, navigate to: **Workflows** ➔ **Import from File** and select `workflow.json`.
3. Configure your API Credentials:
   - **OpenAI API Key**
   - **Airtable Personal Access Token**
4. Update the `Base ID` and `Table ID` in the Airtable nodes with your own Airtable parameters.
5. Toggle the workflow to **Active** (top right corner).

---

## 👤 Author

**Michał Krzemiński**  
*AI & Automation Developer*  
- LinkedIn: https://www.linkedin.com/in/micha%C5%82-krzemi%C5%84ski-2052b6428/
- GitHub: https://github.com/MichaelFlint
