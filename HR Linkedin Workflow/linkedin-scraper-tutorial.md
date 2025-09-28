# 🚀 LinkedIn HR Assistant - Complete Setup Tutorial

## Overview
This n8n workflow automates LinkedIn candidate search and analysis for HR managers. It finds profiles based on job requirements, analyzes them with AI, and saves results to Google Sheets.

### What You'll Need:
- n8n instance (self-hosted or cloud)
- Google account
- OpenAI account
- APIFY account (provides $5 free credit)
- About 30 minutes for setup

---

## 📥 Step 1: Install n8n

### Option A: Cloud Version (Easiest)
1. Go to [https://n8n.partnerlinks.io/5usz6npozak4](https://n8n.partnerlinks.io/5usz6npozak4)
2. Click "Start for free"
3. Create your account
4. You'll get a hosted n8n instance ready to use

### Option B: Self-Hosted
```bash
# Using npm
npm install n8n -g
n8n start

# Using Docker
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

Access n8n at: `http://localhost:5678`

---

## 📋 Step 2: Import the Workflow

1. Copy the workflow JSON file (provided separately)
2. In n8n, click the menu (three lines) in the top-left
3. Select "Workflows" → "Import from File" or "Import from URL"
4. Paste the JSON content or upload the file
5. Click "Import"

The workflow will appear with all nodes and sticky notes ready for configuration.

---

## 🔑 Step 3: Set Up API Credentials

### 3.1 OpenAI API Key

**Purpose:** Powers the AI to generate search keywords and analyze candidates

1. Go to [https://platform.openai.com/](https://platform.openai.com/)
2. Sign up or log in
3. Navigate to [https://platform.openai.com/api-keys](https://platform.openai.com/api-keys)
4. Click "Create new secret key"
5. Name it (e.g., "n8n LinkedIn Assistant")
6. Copy the key immediately (you won't see it again!)

**Add to n8n:**
1. In the workflow, click on any OpenAI node
2. Click on "Credentials" dropdown
3. Select "Create New"
4. Paste your API key
5. Name it "OpenAI account"
6. Click "Save"

---

### 3.2 Google Custom Search API

**Purpose:** Searches Google for LinkedIn profiles

#### Part A: Create Custom Search Engine
1. Go to [https://programmablesearchengine.google.com/](https://programmablesearchengine.google.com/)
2. Click "Add" or "Get started"
3. Configure your search engine:
   - **Search the entire web:** Toggle ON
   - **Name:** "LinkedIn Profile Search"
4. Click "Create"
5. Copy your **Search engine ID** (looks like: a5563873d4aad4c46)
6. Save this ID - you'll need it!

#### Part B: Enable API and Get Key
1. Go to [https://console.cloud.google.com/](https://console.cloud.google.com/)
2. Create a new project or select existing one
3. Click "Enable APIs and Services"
4. Search for "Custom Search API"
5. Click on it and press "Enable"
6. Go to "Credentials" in the left menu
7. Click "Create Credentials" → "API Key"
8. Copy the API key

**Add to n8n:**
1. In the workflow, click the "Google Custom Search" node
2. In credentials, select "Create New"
3. Choose "Header Auth"
4. Set:
   - **Name:** "Google Custom Search"
   - **Header Name:** `key`
   - **Header Value:** Your API key
5. Click "Save"
6. In the node settings, update the `cx` parameter with your Search Engine ID

---

### 3.3 APIFY Account

**Purpose:** Scrapes detailed LinkedIn profile information

**🎁 Note:** APIFY provides $5 free credit for new accounts - enough for ~500 profile scrapes!

1. Go to [https://apify.com/](https://apify.com/)
2. Click "Sign up for free"
3. Complete registration
4. Go to Settings → Integrations
5. Find "Personal API tokens"
6. Copy your API token

**Find the LinkedIn Scraper:**
1. Go to [APIFY Store](https://apify.com/store)
2. Search for "Mass LinkedIn Profile Scraper with Email"
3. Note the actor ID (shown in the workflow as: 2SyF0bVxmgGr8IVCZ)

**Add to n8n:**
1. Click the "Run an Actor" node
2. In credentials, select "Create New"
3. Choose "OAuth2"
4. Enter your API token
5. Name it "Apify account"
6. Click "Save"

---

### 3.4 Google Sheets

**Purpose:** Stores the analyzed candidate data

1. Ensure you're logged into your Google account
2. Create a new Google Sheet or use existing one
3. Name it "LinkedIn Candidates" or similar

**Add to n8n:**
1. Click the "Save to Google Sheet" node
2. In credentials, select "Create New"
3. Choose "OAuth2"
4. Click "Connect my account"
5. Authorize n8n to access Google Sheets
6. Select your spreadsheet from the dropdown
7. The workflow will create necessary columns automatically

---

## ⚙️ Step 4: Configure the Workflow

### 4.1 Update Form Webhook URL
1. After importing, the form will have a unique webhook URL
2. Find it in the "HR Job Search Form" node
3. This is where users will access the form

### 4.2 Verify Node Connections
- All nodes should be connected (green lines)
- Check that each node has valid credentials (green checkmark)

### 4.3 Test the Workflow
1. Click "Execute Workflow" button
2. Open the form URL in a browser
3. Fill in test data:
   - Job Title: "Software Engineer"
   - Location: "Morocco"
   - Number of Profiles: "5"
4. Submit and monitor the execution

---

## 🎯 How to Use the Workflow

1. **Access the Form:** Share the webhook URL with HR team members
2. **Fill Job Requirements:** 
   - Job title (required)
   - Skills (optional)
   - Experience level
   - Location (defaults to Morocco)
   - Number of profiles (5-20)
3. **Submit and Wait:** The workflow will:
   - Generate search keywords
   - Search Google for LinkedIn profiles
   - Scrape detailed information
   - Analyze fit with AI
   - Save to Google Sheets
4. **Review Results:** Check the Google Sheet for:
   - Candidate details
   - AI scoring (1-100)
   - Recommendations
   - Interview questions

---

## 💡 Tips & Best Practices

### Rate Limits
- Google Custom Search: 100 queries/day (free tier)
- APIFY: $5 credit ≈ 500 profiles
- OpenAI: Depends on your plan
- The workflow includes 2-second delays to respect rate limits

### Optimizing Costs
- Start with 5-10 profiles per search
- Use specific job titles for better results
- Monitor your API usage regularly

### Troubleshooting
- **No results found:** Check if location is too specific
- **APIFY timeout:** Increase wait time in node settings
- **Google Sheets error:** Re-authenticate credentials
- **API limits:** Check your quotas in respective dashboards

---

## 🔒 Security Notes

- Never share your API keys publicly
- The workflow JSON has been cleaned of all personal credentials
- Each user must add their own API keys
- Store credentials securely in n8n's credential manager

---

## 📚 Additional Resources

- [n8n Documentation](https://docs.n8n.io/)
- [n8n Community Forum](https://community.n8n.io/)
- [OpenAI Pricing](https://openai.com/pricing)
- [Google Custom Search Pricing](https://developers.google.com/custom-search/v1/overview)
- [APIFY Documentation](https://docs.apify.com/)

---

## 🤝 Support

If you encounter issues:
1. Check the n8n execution logs for errors
2. Verify all API credentials are correct
3. Ensure you haven't hit rate limits
4. Join the n8n community forum for help

---

