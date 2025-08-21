### n8n Workflow Collection

This repository contains a collection of n8n workflows designed to automate various tasks, including social media posting and daily news updates. Each workflow is contained within its own folder, complete with a detailed `README.md` and the workflow's `.json` file.

## Workflows

| Folder | Description |
| :--- | :--- |
| **`Discord n8n Workflow Bots`** | Contains workflows for an AI-powered daily news Discord bot. It fetches the latest news from predefined YouTube channels, summarizes the content, and posts it to a designated Discord channel, preventing duplicate posts using a Google Sheet. |
| **`LinkedIn Image Post with Comments + Image Generation`** | This workflow automates the creation and publishing of engaging LinkedIn posts. It uses a Google Sheet for content ideas, leverages an AI model to generate a post hook and follow-up prompts, and then automatically posts a carousel with an image and adds the prompts as comments for increased engagement. |

## Getting Started

1.  **Clone the Repository:** Clone this repository to your local machine.
2.  **Navigate to a Workflow:** Choose a workflow you are interested in and navigate to its folder.
3.  **Read the `README.md`:** Open and read the `README.md` file in that folder for specific instructions on prerequisites, setup, and how the workflow works.
4.  **Import to n8n:** Import the `.json` file into your n8n instance and follow the instructions to configure your credentials and templates.

## Customization

Each workflow can be customized to fit your specific needs. Refer to the `Customization` section in each workflow's `README.md` to learn how you can adjust the AI models, schedules, and other settings.

## License

This is for you to use. Free and Open Source
