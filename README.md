# Job Search Automation with n8n
Automated job search workflow built with n8n. Prioritizes, ranks, and tracks job postings using custom logic and integration with LinkedIn and RSS feeds.
---
This workflow automates and streamlines my job search using [n8n](https://n8n.io/). It pulls job listings from RSS feeds, filters and scores them, and stores structured job data in Google Sheets. I built this to save time, reduce manual work, and demonstrate my ability to design real-world automation with AI, APIs, and no-code tools.

> ⚠️ **This is a redacted version.** Personal document links, API credentials, and private RSS feeds have been removed for security.

---

**🛠 Built with**  
n8n • JavaScript (custom nodes) • Google Sheets • OpenAI API • rss.app

---

## 🔧 Key Features

- **Automated Job Ingestion**  
  Pulls listings from curated LinkedIn and RSS feeds

- **Smart Filtering**  
  Includes roles like “associate” or “analyst”; excludes “senior” or “director”

- **De-Duplication**  
  Filters out previously seen job posts using extracted Job IDs

- **AI Metadata Extraction**  
  Uses OpenAI to summarize listings, extract structured data, and generate tailored cover letters

- **Resume Matching**  
  Compares each job post with parsed resume data and assigns a skill match score

- **Google Sheets Integration**  
  Centralizes results in a structured, searchable tracker

---

## 📁 Workflow Overview

- **Feed Sources**: Aggregated via `rss.app`
- **Filtering Logic**: JavaScript node with include/exclude keywords
- **Data Output**: Google Sheets + OpenAI enrichment
- **Caching Layer**: Prevents duplicate processing of known jobs/resumes

---

## 🚀 Getting Started

To customize or run this yourself, you’ll need:

- An active [n8n](https://n8n.io/) instance (self-hosted or cloud)
- Your own RSS feed links (replace the placeholders)
- Google Sheets and OpenAI API connections set up in n8n

Then import `Job_Automation_Sanitized.json` into your n8n instance and connect your credentials.
