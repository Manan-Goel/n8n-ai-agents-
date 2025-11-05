🤖 n8n AI Automation Suite

A unified collection of five intelligent automation workflows built on self-hosted n8n (Docker) — combining AI, APIs, and data pipelines to power real-world agentic systems.

These projects demonstrate my ability to design and orchestrate multi-agent systems, integrate APIs, automate workflows, and leverage AI models for scalable business use cases.

⚙️ Deployment Environment

This suite is developed for a Docker-based self-hosted n8n setup.

🐳 Quick Setup

To get the environment running quickly, use the following commands.

# 1. Pull the latest n8n image from Docker Hub
docker pull n8nio/n8n:latest

# 2. Run the n8n container, mapping local ports and persisting configuration
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n


Once the container is running:

Open your browser at http://localhost:5678.

Import the .json workflows provided in the suite.

Configure your local credentials for Ollama, Qdrant, and any other services used within the workflows.

🧩 Project Overview
#	Project Name	Description	Key Integrations
1	TikTok Content Analyzer	Automates trending content research on TikTok using Apify, Gemini AI, and Airtable.	Airtable, Google Drive, Apify API, Gemini AI
2	PDF QnA Agent (RAG System)	Upload PDFs → extract text → embed → store → answer questions locally using Ollama & Qdrant.	FastAPI, Ollama, Qdrant, Webhooks
3	Multi-AI Content Creator	Turns a campaign topic into researched blog, tweet, and LinkedIn post using Tavily + OpenAI.	Tavily API, Google Sheets, OpenAI, LangChain
4	Customer Support AI Agent	Intelligent support system that classifies tickets, fetches context, and drafts responses via AI.	Circle API, Airtable, OpenAI
5	Price Tracker & Market Notifier	Scrapes product prices, analyzes trends, and sends alert emails or Slack messages automatically.	Scrapfly API, Google Sheets, Slack API


            ┌─────────────────────────────────────────────────────┐
            │                      n8n Core                       │
            │─────────────────────────────────────────────────────│
            │  1️⃣  Webhooks & Triggers (HTTP / Cron / Sheet)      │
            │  2️⃣  Data Collection (Scrapers / APIs)              │
            │  3️⃣  Processing (Python APIs / LLM Agents)          │
            │  4️⃣  Storage (Airtable / Qdrant / Sheets / Drive)   │
            │  5️⃣  Notifications (Slack / Email / Telegram)       │
            └─────────────────────────────────────────────────────┘

Each workflow is modular — you can connect, extend, or stack them to form complete AI-driven automation systems (e.g., content operations, data pipelines, or intelligent support bots).

🧱 Project Details (High-Level)
1️⃣ TikTok Content Analyzer

Crawls trending TikTok data using Apify API.

Cleans, sorts, and stores data in Airtable.

Uses Gemini AI to analyze video style, hook, tone, and category.

Uploads downloaded videos to Google Drive and updates insights automatically.

🔁 Runs weekly via Cron trigger.

2️⃣ PDF QnA Agent (RAG System)

Upload PDFs via Webhook.

Extracts text, chunks it, and generates embeddings (Ollama).

Stores embeddings in Qdrant Vector DB.

Responds to natural language questions via another Webhook, retrieving top chunks and generating answers using LLaMA 3.2.

💬 Acts as a self-contained local document AI.

3️⃣ Multi-AI Content Creator

Reads new campaign topics from Google Sheets.

Uses Tavily API to collect recent information on the topic.

Passes context to multiple LangChain agents:

🧩 LinkedIn Post Agent

🧩 Twitter/X Post Agent

🧩 Blog Writer Agent

Writes final outputs back to the sheet.

⚙️ Enables automated marketing content production.

4️⃣ Customer Support System

Fetches support tickets from Circle or Airtable.

Uses AI classifier to tag and prioritize tickets.

Pulls context (user history, tone) from connected databases.

Drafts response templates using OpenAI GPT.

Sends updates via Email or Slack notifications.

🎯 Ideal for streamlining repetitive customer queries.

5️⃣ Price Tracker & Market Notifier

Scrapes product data from e-commerce sites via Scrapfly API.

Analyzes historical prices and deltas using LLM summarization.

Logs data into Google Sheets.

Sends notifications via Slack or email when:

Price drops > threshold

Stock status changes

📈 Automates e-commerce price intelligence.


🧠 AI Models & APIs Used

| Model / API                              | Purpose                              |
| ---------------------------------------- | ------------------------------------ |
| **Gemini 1.5 Pro**                       | TikTok video content analysis        |
| **OpenAI GPT-4 / LangChain Agents**      | Multi-role content generation        |
| **Ollama (nomic-embed-text, LLaMA 3.2)** | Local embeddings + answer generation |
| **Tavily Search API**                    | Real-time content research           |
| **Scrapfly API**                         | Web scraping for product prices      |
| **Apify API**                            | TikTok data crawling                 |
| **Airtable / Qdrant / Google Sheets**    | Data persistence & storage           |


🧰 Setup & Configuration

| Service           | Credential Name     | Type                  |
| ----------------- | ------------------- | --------------------- |
| Airtable          | `airtable_api`      | Personal Access Token |
| Google Sheets     | `google_oauth`      | OAuth                 |
| Gemini / OpenAI   | `ai_api_key`        | API Key               |
| Tavily / Scrapfly | `api_access`        | API Key               |
| Slack             | `slack_bot_token`   | OAuth                 |
| Qdrant            | `qdrant_connection` | HTTP / API Key        |
| Circle            | `circle_api`        | API Key               |


Each workflow uses environment variables or expressions like:
{{$env.AIRTABLE_API_KEY}}
{{$json["data"]["id"]}}
{{$node["HTTP Request"].json["response"]}}


🚀 How to Run

Start FastAPI Microservices (for data crawl or cleaning):

uvicorn crawl_api:app --host 0.0.0.0 --port 8001 --reload
uvicorn clean_api:app --host 0.0.0.0 --port 8002 --reload

Run n8n container

docker start n8n

Import Workflows

Go to Workflows → Import from File

Upload each .json file

Add Credentials under Settings → Credentials

Execute / Schedule workflows from the UI

🧩 Outcome

This suite transforms n8n into a full-fledged AI Automation Engine — capable of running data collection, cleaning, LLM-powered reasoning, and notification systems without manual intervention.

🧑‍💻 Author

Manan
AI & Automation Developer
📧 Email: manangoel682@gmail.com • 🌐 GitHub: https://github.com/Manan-Goel


⭐ If you found this project useful, don’t forget to star the repo and share feedback!
