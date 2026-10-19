# What is this?

WoopSocial's MCP is a **remote** MCP server that allows your AI agent to post or schedule posts to various social media platforms such as Facebook, Instagram, LinkedIn, Pinterest, YouTube, TikTok, X/Twitter and more.

It is a remote MCP server, which has the benefit of not requiring you to install any additional software on your computer apart from the AI agent(s) that you already have.

# Claude plugin

This repository is also a Claude plugin. It adds the WoopSocial connector and a `publish-posts` skill that teaches Claude the posting workflow: resolve the project and connected accounts, upload media, validate the post, then publish or schedule it and report how it was delivered.

1. Create a WoopSocial account [here](https://woopsocial.com/).
2. Add the WoopSocial plugin in Claude, then connect WoopSocial from the plugin's Connectors tab and sign in. No API key is needed.
3. Ask Claude to post, for example: "Schedule this video to TikTok, YouTube and Instagram for Friday at 18:00."

# Quickstart

1. Create a WoopSocial account [here](https://woopsocial.com/).
2. Create an API key [here](https://app.woopsocial.com/api-access).
3. Copy the MCP URL from the dialog shown after the API key is created.
4. Add the MCP URL to your favorite AI agent.
    1. Claude Code:
        ```bash
        claude mcp add --transport http woopsocial "https://api.woopsocial.com/mcp?api_key=YOUR_API_KEY"
        ```

        Note: As an alternative, Claude Code also supports our OAuth-based authentication flow. Details are available in the [Claude Code CLI integration guide](https://docs.woopsocial.com/mcp/integrating-clients#claude-code-cli).

    2. Codex:
        ```bash
        codex mcp add woopsocial --url "https://api.woopsocial.com/mcp?api_key=YOUR_API_KEY"
        ```
    
    3. See our [Integrating MCP clients](https://docs.woopsocial.com/mcp/integrating-clients#integrating-mcp-clients) guide for more clients.

5. Ask your AI agent something about WoopSocial in natural language, for example: "List my social accounts connected to WoopSocial" or "Generate and schedule 10 posts for my business on X via WoopSocial". Your AI agent will use the appropriate [tools](https://docs.woopsocial.com/mcp/tools-reference) of our MCP to complete the task.

# Data

The plugin itself runs no code and stores nothing. Claude sends the post content, schedule and selected accounts to your WoopSocial account through `api.woopsocial.com`, and uploads media to presigned URLs on `r2.cloudflarestorage.com`. WoopSocial then publishes to the social platforms you connected.

# Support

If you encounter any issues, please send us an email to `contact@woopsocial.com` or feel free to open an issue in this repo.