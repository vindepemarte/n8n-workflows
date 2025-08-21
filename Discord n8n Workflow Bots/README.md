# AI & Open-Source Daily News Discord Bot

This repository contains an n8n workflow that automates the discovery and sharing of the latest AI news and open-source resources. The workflow is designed to run daily, fetching new content, summarizing it, and posting it to a Discord server. It also uses a Google Sheet to keep track of already-shared links, preventing duplicate posts.

The workflow is split into two main, independent branches: one for AI news and another for open-source resources.

## Features

- **Automated Scheduling:** The workflow runs daily at a specific, pre-set time.
- **Content Discovery:** Uses the Google Custom Search API to find the latest videos from a list of predefined YouTube channels and the latest open-source projects.
- **Duplicate Prevention:** Checks a Google Sheet to ensure that a link has not been shared before.
- **Intelligent Summarization:** Leverages the Gemini AI model to summarize video descriptions and project notes.
- **Automated Posting:** Publishes a formatted, professional-looking message to a designated Discord channel.

## Workflow Overview

The n8n workflow consists of two primary sections:

1.  **AI Daily News Bot:**
    - Triggered daily at **8 AM**.
    - Searches for new videos from YouTube channels about AI.
    - Checks for duplicates in a Google Sheet.
    - Summarizes the video's content using the Gemini AI model.
    - Appends the new video's URL and summary to the Google Sheet.
    - Posts an embedded message to a Discord channel.

2.  **Open Source Resources Bot:**
    - Triggered daily at **9 AM**.
    - Searches for new open-source AI projects on GitHub.
    - Checks for duplicates in a separate Google Sheet.
    - Summarizes the project using the Gemini AI model.
    - Appends the new project's URL, topic, and notes to the Google Sheet.
    - Posts an embedded message to a Discord channel.

## Prerequisites

Before you can set up this workflow, you need to have the following:

- An **n8n instance** (self-hosted or cloud).
- A **Google Cloud account** to get a Custom Search API key and a Search Engine ID.
- A **Google Sheets account** with a dedicated spreadsheet for logging.
- A **Discord server** and a Discord Bot with permissions to post messages and embeds.
- An **OpenRouter account** (or a similar service) to access the Gemini AI model.
- An **n8n account** with the necessary credentials configured.

## Setup Instructions

### 1. Configure Credentials

In your n8n instance, you must configure the following credentials:

-   **Google Sheets OAuth2 API:**
    -   Follow the [n8n Google Sheets documentation](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googleSheets/) to set up an OAuth2 credential. This will give the workflow permission to read from and write to your Google Sheet.

-   **Google Custom Search API:**
    -   You need a **Google API Key** and a **Custom Search Engine ID (CX)**. You can get these by following the official [Google Custom Search API guide](https://developers.google.com/custom-search/v1/overview).
    -   In the n8n `GSearch` and `GSearchO` nodes, enter your API key and CX ID in the `queryParameters`.

-   **Discord Bot API:**
    -   Follow the [n8n Discord documentation](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.discord/) to create a Discord bot and get your bot token.
    -   Create a new Discord Bot API credential in n8n.

-   **Gemini (or other LLM) API:**
    -   This workflow uses the Gemini model via OpenRouter.
    -   Create an **OpenRouter API credential** in n8n and add your API key.

### 2. Prepare the Google Sheet

Create a new Google Sheet with two separate tabs (worksheets):

1.  **Tab 1: `ai-hot-daily`**
    -   Create columns with the exact headers: `URL` and `SumDescription`.

2.  **Tab 2: `open-source-resource`**
    -   Create columns with the exact headers: `URL`, `Topic`, and `Notes`.

### 3. Import and Configure the Workflow

1.  Copy the JSON code from the `workflow.json` file in this repository.
2.  In your n8n instance, go to the **Workflows** page and click **New**.
3.  In the top-right corner, click the **three dots** and select **Import from JSON**. Paste the JSON code and click **Import**.
4.  Once imported, you must update each node with your specific information:
    -   **Discord Nodes (`Send ai-hot-daily-news` and `Send open-source-corner`):** Select your Discord Bot credential and the correct Discord server and channel IDs.
    -   **Google Sheets Nodes (`GSheetCheck`, `GSheetAdd`, `GSheetOCheck`, `GSheetOAdd`):** Select your Google Sheets credential and the correct Document ID and Sheet Name for each node.
    -   **AI Agent Nodes (`Channels and Summarise Agent` and `Open Source Agent`):** Connect the AI Language Model nodes to the agent nodes.

### 4. Activate the Workflow

After you have configured all the nodes and connected the credentials, save the workflow. To enable the automated runs, toggle the **"Active"** switch in the top-right corner of the workflow editor.

The workflow will now run on its set schedule, providing daily updates to your Discord server!

---

**Disclaimer:** This workflow is a starting point. Feel free to customize it to fit your needs, such as adding more content sources, changing the posting schedule, or modifying the prompts to alter the summarization style.
