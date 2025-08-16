# Automated Job Search Workflow (n8n + OpenAI + Google Sheets)
**Version 4 — Targeted Filtering and Higher-Fit Role Prioritization**

<picture>
  <img src="https://github.com/user-attachments/assets/61f9663d-570c-4459-b5dd-089c562e148b" width="20" height="20" alt="Notion logo" />
</picture>
<strong>Notion Walkthrough:</strong>
Explore the full breakdown of this project across v1 → v4 with diagrams, screenshots, notes, metrics, and lessons learned:

👉 [View my full project in Notion](https://working-knuckle-420.notion.site/n8n-Job-Search-Assistant-248b1441915d8047a5a6d67c81a91ddc)

## Overview
This workflow automates the sourcing, filtering, enrichment, and ranking of job postings in San Francisco’s tech sector. It specifically targets business operations, product operations, and project coordination roles that align with my transferable experience.

Originally built to support my transition from high-performance kitchen operations into tech, the system now includes a two-stage seniority filter: an initial keyword/date pass early in the pipeline, and a new strict if node later that removes any senior roles before resume parsing and scoring. This ensures only relevant, achievable roles make it to the application stage.
> ⚠️ **This is a redacted version.** Personal document links, API credentials, and private RSS feeds have been removed for security.

### 🔧 The system:
1. **Collects** postings from targeted RSS feeds for selected tech companies.  
2. **Filters** irrelevant and senior level roles before processing.  
3. **Deduplicates** jobs already stored in Notion.  
4. **Enriches** job data with company metadata, keywords, and technical/functional skill extraction using GPT.
5. **Applies strict seniority filters** to remove any remaining senior roles 
6. **Parses** my resume into structured JSON for matching.  
7. **Scores** job fit using a weighted model for hiring likelihood (experience level, role alignment, technical barrier, and company signals). 
8. **Generates** tailored, ATS friendly base cover letter.  
9. **Updates** Notion database for centralized tracking
---
## 🛠️ Technical Improvements

###  Key Improvements in v2
- **Improved Job Data Collection -** Expanded extracted fields to include role descriptions, functional keywords, technical skills, and richer company metadata.
- **Updated Ranking System for Skill Alignment -** Rebuilt the scoring logic to weight technical overlaps and domain fit more heavily, ensuring high scores only go to truly relevant roles.
###  Key Improvements in v3
- **RSS Rate Limiting -** Staggered RSS feed collection to respect RSS.app service limits.
- **Fixed Loop Conflicts -** Resolved Split in Batches timing issues that caused incomplete processing.
###  Key Improvements in v4
- **Notion Integration -** Replaced Google Sheets tracking with a Notion database for richer search, filtering, and dashboarding
- **Two-Stage Seniority Filtering -** Added a new strict if node after job enrichment to catch and remove any senior roles that pass the initial keyword/date filter.
---
## 🐣 Project Evolution

| Version  | Focus                           | Key Improvements |
|----------|----------------------------------|------------------|
| **🥚 v1** | Initial Automation               | - Basic RSS feed ingestion  <br> - Simple filtering and skill matching <br> - Resume parsed via HTTP  <br> - Basic Google Sheets logging |
| **🐥 v2** | Enhanced Data & Reliability      | - Switched to Google Docs API for cleaner resume data <br> - Improved job metadata extraction <br> - Expanded filtering logic to reduce noise <br> - Upgraded to 1–5+ ranking system |
| **🐓 v3** | Precision Scoring and Processing (Current)      | - Fully redesigned ranking logic focused on hiring likelihood <br> - Fixed RSS batch processing and sequential job handling <br> - Improved API cost control and error handling <br> - Simplified back to 1–5 scale for clearer prioritization |
| **🍗 v4** | Notion Integration & Filtering              | - Notion API storage <br> - Senior role exclusion via if node <br> - Normalized seniority outputs |


---
## 🧰 Tech Stack
- **n8n -** workflow automation  
- **RSS Feeds -** company job listings  
- **OpenAI API -** data extraction, enrichment, and cover letter generation  
- **Notion API -** data storage and visualzation  
- **Google Docs API -** direct resume retrieval  
- **JavaScript -** custom filtering, caching, and data transformation  

---

## 📐 Workflow Architecture

RSS Feeds (Rate Limited)  
→ Initial Role & Seniority Filtering  
→ Deduplication by Job ID in Notion  
→ Job Data Enrichment (metadata + skill extraction)  
→ Strict Seniority Filter  
→ Sequential Job Processing:  
&nbsp;&nbsp;&nbsp;→ Resume Retrieval via Google Docs API  
&nbsp;&nbsp;&nbsp;→ Precision Fit Scoring  
&nbsp;&nbsp;&nbsp;→ Cover Letter Generation  
→ Google Sheets Update  

---

## 🖼️ Visual Overview

### Detailed Workflow Diagram  
A high-level, color-coded breakdown of the full automation flow:

![Detailed Workflow](Media/diagram-detailed.png)

---

### Real Workflow from n8n  
Here’s the live view from my n8n instance, showing the full node structure:

![n8n Screenshot](Media/Workflow-light-v4.png)

---

## 📚 Lessons Learned
- Stronger front-end filtering saves time, tokens, and reduces noise.
- Direct API connections (Google Docs) are more reliable than scraping.  
- A clean caching system improves stability and efficiency.  
- Ranking logic must be customized to your pivot.
- Data normalization is key for downstream processing and filtering.

---

## 🚀 How to Run Locally
> ⚠️ **This repo contains multiple versions of the workflow.** For the most recent and recommended setup, use n8n Job_Search_Automation_v3.json. Version 1, and 2 are included for historical reference.
1. Clone this repo.  
2. Import `Job_Search_Automation_v3.json` into n8n.  
3. Add environment variables:  
   - `OPENAI_API_KEY`  
   - Google API credentials **Docs**
   - Notion API and database ID
4. Replace RSS feed URLs with your own target company feeds.  
5. Trigger manually or schedule daily runs.  

---

## 📊 Example Output

| Title                         | Company Name | Location           | Score | Link | Cover Letter            |
|--------------------------------|--------------|--------------------|-------|------|-------------------------|
| Product Operations Coordinator | Airtable     | San Francisco, CA  | 3    | View | Generated, ATS-ready    |

---

## ➡️ Next Steps
- Integrate alerts for high-scoring roles.
