# Automated Job Search & Cover Letter Generator with n8n and Google Gemini

## Project Overview

This project automates the entire job search and application workflow using n8n, Google Gemini (PaLM), and Google Sheets. It streamlines fetching relevant job listings, analyzing and scoring each job based on your profile, generating personalized cover letters, and tracking all applications in a centralized Google Sheet. Additionally, it sends daily email summaries of top job matches, helping you apply efficiently and systematically.

---

## Features

- **Scheduled daily job search:** Automatically runs every morning to fetch the newest job listings from a configured RSS feed.
- **Job data extraction & normalization:** Uses Google Gemini AI to parse and structure job details from raw web pages.
- **Match scoring:** Custom AI scoring of how well each job fits your skills and experience.
- **Personalized cover letter generation:** Automatically produces tailored cover letters for each job using Gemini AI.
- **Data storage & tracking:** Appends or updates job information, scores, and cover letters in a Google Sheet.
- **Email notifications:** Sends daily summaries or individual application emails via Gmail integration.
- **Duplicate prevention:** Matches on job URL to avoid repeated entries in Google Sheets.

---

## How It Works (Workflow Breakdown)

1. **Schedule Trigger:** Activates the workflow every day at the configured hour (e.g., 8:00 AM).
2. **RSS Job Feed Read:** Pulls new job listings from the configured RSS feed.
3. **Limit Node:** Restricts the number of jobs processed in each run to control API usage.
4. **HTTP Request:** Fetches full job details by accessing the job posting URL.
5. **Google Gemini (Job Parsing):** Extracts structured job information (company, role, benefits, description, contact, etc.) in JSON.
6. **Data Cleaning:** Parses and validates the AI output to ensure correct JSON format.
7. **Google Gemini (Match Scoring):** Scores how closely the job fits the candidate’s skills and experience, returning a normalized score.
8. **Score Parsing:** Cleans and formats the scoring output.
9. **Google Gemini (Cover Letter):** Generates a customized cover letter specific to the job and candidate profile.
10. **Cover Letter Parsing:** Validates the AI-generated cover letter JSON output.
11. **Google Sheets Integration:** Adds or updates the job data, match score, and cover letter into a Google Sheet for tracking.
12. **Email Sending:** Sends the personalized cover letter to the recruiter or specified contact at the company.

---

## Setup Instructions

### Prerequisites

- n8n installed and accessible (self-hosted or via n8n cloud)
- Google Cloud API credentials for Gemini (PaLM) API access
- Google Sheets API credentials with a sheet created for storing job data
- Gmail OAuth2 credentials for sending email notifications
- RSS feed URL of your preferred job listings source (Google Jobs, Indeed, or similar)

### Configuration

1. Import the provided n8n workflow JSON file into your n8n instance.
2. Configure the credentials for:
   - Google Gemini API node (PaLM API)
   - Google Sheets node (Google Sheets API OAuth)
   - Gmail node (Gmail OAuth2)
3. Update the RSS feed URL node if you want a different job source.
4. Set your preferred daily schedule time in the Schedule Trigger node.
5. Update the candidate profile and skills in the match scoring Gemini prompt within the workflow.
6. Customize email templates if needed in the Gmail node.

### Running Locally

- Run n8n locally or deploy to a server.
- Ensure all API keys and OAuth credentials are securely stored and linked in n8n.
- Activate the workflow to enable scheduled automation.

---

## Prompts & API Usage

- **Job Parsing Prompt:** Extracts key company and job details in JSON, limiting description length and formatting consistently.
- **Match Scoring Prompt:** Compares your detailed resume with the job description to generate a compatibility score out of 5.
- **Cover Letter Prompt:** Uses your profile and job details to create a personalized, professional cover letter returned as JSON.
- **API Nodes:** Use Google Gemini for NLP tasks, Google Sheets to store results, and Gmail for notifications.

---

## Challenges & Solutions

| Challenge                  | Solution                                                               |
|----------------------------|------------------------------------------------------------------------|
| API Rate Limits            | Limiting processed jobs per run and scheduling to avoid excess calls.  |
| Parsing Varied Job Content | Custom AI prompts to standardize data extraction to JSON format.        |
| Gemini Output Variability  | Multiple validation nodes to parse and clean JSON from AI responses.    |
| Duplicate Job Entries      | Matching on job URL in Google Sheets to update instead of duplicate.    |
| Personalization            | Embedding static resume info into prompts to tailor cover letters.      |
| Email Deliverability       | Gmail OAuth2 integration to securely send email notifications.          |

---

## Summary of Learnings

- Automating job applications can save hours while increasing quality and consistency.
- Strong prompt engineering with Google Gemini is crucial for reliable, structured output.
- Integrating AI with workflow tools like n8n enables scalable, personalized automation.
- Data cleaning and handling edge cases in AI-generated text is necessary for robustness.
- Leveraging Google Sheets provides an accessible, centralized tracking system.
- Email automation keeps you promptly informed and ready to engage with top matches.

---

## License

This project is open source and available under the MIT License.

---

## Author

Jatin Kanyan

---

## Screenshots & Demos

*(Add screenshots for the n8n workflow, example Google Sheet, and sample email notifications here once available)*

---

## Contributions & Feedback

Contributions, issues, and feature requests are welcome. Feel free to fork the repo and create pull requests or open issues for discussion.
