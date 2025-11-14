# AI-Powered Website Tech Stack Analyzer with n8n

This project is an n8n automation workflow that uses AI (OpenAI) to automatically analyze the technological stack of websites (domains) listed in a Google Sheet and save the results back to the same sheet.

It takes a list of domains as input, categorizes the technologies they use (such as CMS, hosting, analytics tools), and writes the findings into their respective columns.

---

## 🚀 Project Goal

The primary goal of this project is to automate the manual, time-consuming process of researching the technology stack of websites. This automation is designed to accelerate processes such as market research, competitive analysis, and lead generation.

## 🛠️ Data Collected

This automation analyzes a website and identifies the following technology categories:

* **Hosting & Server:** (e.g., "AWS servers", "Facebook Infrastructure")
* **Analysis & Tracking Tool:** (e.g., "Facebook Analytics", "Meta Pixel")
* **Security & Performance:** (e.g., "256-bit SSL certificate", "HSTS")
* **Other Technologies:** (e.g., "Email marketing", "SEO-friendly themes", "Meta AI")
* **CMS & Content Management:** (e.g., "ikas e-commerce platform", "Shopify", "Facebook CMS")

## ⚙️ Workflow Steps

The automation follows these steps within the n8n workflow:

1.  **Google Sheets - Get row(s):**
    Reads all domains listed in the `Company Domain` column from the specified Google Sheet.

2.  **Loop Over Items:**
    Starts a loop to process each domain individually.

3.  **HTTP Request:**
    Sends an HTTP request to the domain to fetch its content or header information.

4.  **AI Agent (OpenAI):**
    Sends the fetched data to the AI model. A "System Prompt" instructs the AI to analyze the site, identify the technologies used, and structure the output as JSON under the pre-defined categories.

5.  **Google Sheets - Append or update row:**
    Takes the structured JSON data from the AI. It uses the `Company Domain` as the "Column to Match On" (the unique key) to:
    * **UPDATE** the row with the new technology data if the domain already exists.
    * **APPEND** the data as a new row at the bottom of the sheet if the domain is not found.

## 🔧 Setup and Usage

To use this workflow:

1.  **Prepare Your Google Sheet:**
    * Create a new Google Sheet.
    * The first column **must** be named `Company Domain`.
    * Name the other columns to exactly match the categories listed above (e.g., `Hosting & Server`, `Analysis & Tracking Tool`, etc.).

2.  **Import the n8n Workflow:**
    * Download the `workflow.json` (or `.n8n.json`) file from this repository.
    * In your n8n canvas, select "Import from File" and upload the workflow.

3.  **Set Up Credentials:**
    * **Google Sheets:** Add your credentials for the Google Sheets API to your n8n instance.
    * **OpenAI:** Add your OpenAI API key to your n8n credentials.

4.  **Configure the Nodes:**
    * **Google Sheets (Get):** Select your credentials, and enter your Sheet ID and sheet name.
    * **Google Sheets (Append or update):** Select your credentials, enter your Sheet ID, sheet name, and—most importantly—set the **"Column to Match On"** field to `Company Domain`.

5.  **Execute:**
    * Add the domains you want to analyze to the `Company Domain` column in your Google Sheet.
    * Click "Execute Workflow" in n8n and watch the results populate your sheet.

## 📄 License

This project is licensed under the MIT License. See the `LICENSE` file for details.
