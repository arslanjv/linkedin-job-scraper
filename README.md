# 📩 LinkedIn Job Scraper & Email Alert

This project automates **LinkedIn job scraping** using [n8n](https://n8n.io) and the **Apify API**. It fetches job postings, formats them into a clean HTML table, and sends email alerts on a schedule.

---

## ✨ Features
- ⏰ **Automated Scheduling**: Runs on a customizable Cron schedule.
- 🌐 **LinkedIn Job Scraping**: Fetches job data via Apify’s API.
- 📊 **Clean Output**: Formats jobs into an HTML table (Job Title, Company, Location, etc.).
- 📧 **Email Alerts**: Delivers job listings to your inbox.
- 🐳 **Docker Support**: Simple setup with Docker Desktop.

---

## 🐳 Setup with Docker Desktop
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/arslanjv/linkedin-job-scraper.git
   cd linkedin-job-scraper
   ```

2. **Run n8n in Docker**:
   ```bash
   docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n n8nio/n8n
   ```

   > Access n8n at: [http://localhost:5678](http://localhost:5678)

3. **Import Workflow**:
   - Open n8n in your browser.
   - Navigate to **Workflows → Import Workflow**.
   - Upload the `Job Scraper + Alert.json` file from the repository.

---

## 🔑 Configure Credentials

### 1. Apify API
- Sign up at [apify.com](https://apify.com) and create an account.
- Find your **API Token** in **Account → Integrations**.
- In n8n, edit the **LinkedIn Job Scraper** node (HTTP Request):
  - Set the **Authorization** header:
    ```
    Bearer <your_apify_token>
    ```
  - Update the **URL** with your [Apify Actor ID](https://apify.com/logical_scrapers/linkedin-jobs-scraper) and copy actor id from url for the LinkedIn Scraper:
    ```
    https://api.apify.com/v2/acts/<your-actor-id>/run-sync-get-dataset-items
    ```
    
### 2. Email (SMTP)
- In n8n, go to **Credentials → Add Credential → SMTP**.
- Configure with your email provider’s settings. Example for Gmail:
  ```
  Host: smtp.gmail.com
  Port: 465
  User: your-email@gmail.com
  Password: your-app-specific-password
  SSL/TLS: Enabled
  ```
  > Note: For Gmail, generate an [App Password](https://myaccount.google.com/security) if 2FA is enabled.
- Assign this credential to the **Send Email** node in the workflow.

---

## ⚙️ Customize Job Filters
Edit the **LinkedIn Job Scraper** node’s request body to set job search preferences:
```json
{
  "keywords": "Cyber Security",
  "location": "Pakistan",
  "maxRows": 10
}
```
- `keywords`: Job role or skill (e.g., "Software Engineer", "Data Analyst").
- `location`: City or country (e.g., "New York", "Remote").
- `maxRows`: Maximum number of jobs to fetch per run (e.g., 10).

---

## 📧 Sample Email Output
The email alert contains a well-formatted HTML table with job details:

<table border="1" cellpadding="8" style="border-collapse: collapse; width: 100%; font-family: Arial, sans-serif;">
  <tr style="background-color: #f2f2f2;">
    <th>Logo</th>
    <th>Job Title</th>
    <th>Company</th>
    <th>Location</th>
    <th>Industry</th>
    <th>Type</th>
    <th>Experience</th>
    <th>Education</th>
    <th>Date Posted</th>
    <th>Valid Through</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>🏢</td>
    <td>Security Analyst</td>
    <td>CyberTech Ltd.</td>
    <td>Lahore, PK</td>
    <td>Information Technology</td>
    <td>Full-Time</td>
    <td>2 years</td>
    <td>BSc Computer Science</td>
    <td>16-Aug-2025</td>
    <td>20-Aug-2025</td>
    <td>Monitor and analyze security incidents, implement protocols...</td>
  </tr>
</table>

---

## 📜 License
MIT License – free to use and modify.

---

## 🙌 Contribute
Contributions are welcome! Submit pull requests or open issues. If you find this project helpful, please ⭐ the repository.
