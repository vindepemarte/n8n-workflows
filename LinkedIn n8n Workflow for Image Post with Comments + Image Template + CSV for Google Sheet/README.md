### LinkedIn Post with Comments Workflow

This repository contains an n8n workflow designed to automate the creation and publishing of engaging LinkedIn posts. The workflow uses a Google Sheet as a source for post ideas, leverages AI to generate content, and then automatically posts a carousel with a hook and adds the prompts as comments for increased engagement.

## Workflow Overview

The core of this workflow is an automated process that runs on a schedule. It pulls a topic idea from a Google Sheet, generates a compelling post using an AI model (like Gemini-2.5-flash), and then posts it to your LinkedIn profile. Finally, it follows up by adding the individual prompts as comments to the post.

Here is a visual representation of the workflow:

## Getting Started

### Prerequisites

To use this workflow, you will need:

  * An n8n account (self-hosted or cloud)
  * A Google Account
  * A LinkedIn Account
  * An OpenRouter account (or another compatible AI API service)

### Step 1: Download the Workflow

Download the `LinkedIn_Post_With_Comments.json` file from this repository.

### Step 2: Set Up Your Data Templates

This workflow relies on two template files: a Google Drive image template and a Google Sheets template.

1.  **Image Template (`.png` file):**
    The workflow uses a Google Drive file named `Iacovici Alexandru.png` as a template for the carousel image. The AI-generated text is written directly onto this image. You can use your own `.png` template, but you will need to update the "Download file" node in the workflow with your file's ID. This image serves as the background for the text.

2.  **Google Sheets Template (`.csv` file):**
    The workflow pulls post ideas from a Google Sheet. A template CSV file named `LinkedIn_7_Amazing_Prompts_Ideas.csv` is included in this repository. You can upload this to Google Sheets or your preferred platform.

      * **Sheet Name:** `Ideas`
      * **Columns:** `Topic Idea` and `Status`
      * The workflow will look for rows where the `Status` column is set to `Not Done`.

## How the Workflow Works

1.  **Schedule Trigger:** The workflow is set to run at specific times (e.g., 7:28 AM, 12:28 PM, 6:28 PM) to ensure a consistent posting schedule.
2.  **Get User Info:** It authenticates with your LinkedIn account to retrieve your user ID.
3.  **Get Idea:** It connects to your Google Sheet and retrieves a single post idea with the status "Not Done".
4.  **Rules:** It sets parameters for the AI agent, including tone, language, and word limits.
5.  **AI Content Generation:** The AI Agent node, using a model like Gemini-2.5-flash, generates a post hook and seven distinct prompts in a structured JSON format.
6.  **Create Image:** The generated hook text is overlaid onto the image template from Google Drive.
7.  **Create a post:** The carousel image is posted to your LinkedIn profile.
8.  **Wait:** The workflow waits for a brief period to ensure the post is live.
9.  **Comment Prompt Loop:** A loop iterates through the seven generated prompts and adds each one as a separate comment to the newly created post.
10. **Update Google Sheet:** The status of the post idea in the Google Sheet is updated to "Done".
11. **Send Email:** A final confirmation email is sent to notify you that the post was published successfully.

## Customization

  * **AI Model:** You can change the AI model by modifying the "Flash" and "Flash-Structure" nodes to use a different provider or model.
  * **Scheduling:** Adjust the "Schedule Trigger" node to match your preferred posting times.
  * **Image Template:** Swap the `Iacovici Alexandru.png` file ID in the "Download file" node with your own custom image template.
  * **Google Sheet:** Modify the "Get Idea" node to point to your specific Google Sheet and sheet name if you've named it differently.
  * **Email Notifications:** Update the "Send a message" node with your email address.
