# WoopSocial

Write, publish and schedule posts to Facebook, Instagram, Threads, LinkedIn, Bluesky, X/Twitter, Pinterest, TikTok and YouTube from a conversation, plan your content, and check how the posts you sent through WoopSocial were delivered and performed, all through your WoopSocial account.

This plugin adds the WoopSocial connector and 17 skills.

**Post and schedule**

| Skill | What it does |
|---|---|
| `publish-posts` | Publish or schedule a post to any connected account and report how it was delivered. |
| `instagram-posts` | Write and schedule Instagram posts, carousels, Reels, Stories and Trial Reels. |
| `tiktok-posts` | Write captions for and schedule TikTok videos and photo carousels, with the right privacy and labels. |
| `linkedin-posts` | Write and schedule LinkedIn posts for a personal profile or a company page. |
| `cross-post-everywhere` | Post one piece of content to every platform at once, adjusted per platform. |
| `bulk-schedule-posts` | Schedule many posts at once from a spreadsheet, CSV, Notion table or a folder of photos and videos. |

**Manage your accounts and queue**

| Skill | What it does |
|---|---|
| `connect-social-accounts` | Connect your social accounts so the assistant can post to them. |
| `manage-post-queue` | See what's scheduled, move or cancel posts, or pause everything and resume later. |
| `fix-failed-posts` | Find posts that didn't go out, explain why, fix them and re-send. |
| `social-media-report` | See how your posts performed and what to post more of. |

**Plan and create**

| Skill | What it does |
|---|---|
| `instagram-carousel-maker` | Write a carousel slide by slide with the caption and a design spec, render simple text slides when code execution is available, then schedule it once the slide images exist. |
| `content-calendar-generator` | Plan a month of posts with captions, then schedule the ready ones and save the rest as drafts. |
| `content-ideas-generator` | Post ideas for your niche, built on your best posts sent through WoopSocial when connected. Picked ideas can be saved as drafts. |
| `social-media-audit` | Review an account and get a ranked fix list and a two-week plan. |
| `weekly-social-autopilot` | Each week: review last week, draft next week in your voice, approve, schedule. |
| `real-estate-instagram-posts` | A week of listing, open house and local posts for real estate agents, scheduled after you approve them. |
| `restaurant-instagram-posts` | A week of menu, specials, events and behind-the-scenes posts for restaurants, cafes and bars. |

The skills that write posts for you show every post before it goes out, and the assistant asks before scheduling several posts at once or deleting, moving or pausing them.

# Getting started in Claude

1. Create a WoopSocial account [here](https://woopsocial.com/) and connect your social accounts.
2. Add the WoopSocial plugin in Claude, then connect WoopSocial from the plugin's Connectors tab (in Claude Code, run `/mcp`) and sign in. No API key is needed.
3. Ask Claude to post, for example: "Schedule this video to TikTok, YouTube and Instagram for Friday at 18:00."

# Other AI agents

The plugin uses WoopSocial's **remote** MCP server at `https://api.woopsocial.com/mcp`, so any MCP client can connect to it with nothing extra to install. There are two ways to sign in:

- **OAuth (recommended):** add the server URL, then sign in to WoopSocial in your browser and click **Authorize**. No API key is needed. This works in Claude, Claude Code, Codex, Cursor and Notion.
- **API key:** for clients that don't support OAuth yet. Create an API key [here](https://app.woopsocial.com/api-access) and copy the MCP URL shown after the key is created. That URL includes your key, so keep it private.

Before you start, create a WoopSocial account [here](https://woopsocial.com/) and connect at least one social account.

1. Claude Code (OAuth):
    ```bash
    claude mcp add --transport http woopsocial "https://api.woopsocial.com/mcp"
    ```

    Then start `claude`, type `/mcp`, select `woopsocial`, choose **Authenticate** and click **Authorize** in your browser.

2. Codex (OAuth):
    ```bash
    codex mcp add woopsocial --url "https://api.woopsocial.com/mcp"
    ```

    ```bash
    codex mcp login woopsocial
    ```

3. Clients without OAuth support: add the MCP URL with your API key, for example:
    ```text
    https://api.woopsocial.com/mcp?api_key=YOUR_API_KEY
    ```

4. See our [Integrating MCP clients](https://docs.woopsocial.com/mcp/integrating-clients#integrating-mcp-clients) guide for step-by-step setup in ChatGPT, Notion, Gemini CLI, Cursor and more.

Then ask your AI agent something about WoopSocial in natural language, for example: "List my social accounts connected to WoopSocial" or "Generate and schedule 10 posts for my business on X via WoopSocial". Your AI agent will use the appropriate [tools](https://docs.woopsocial.com/mcp/tools-reference) of our MCP to complete the task.

# Data

The plugin ships no code of its own and stores nothing. To upload media or render carousel slides, the assistant may run commands in your code execution environment or shell. The post content, schedule and selected accounts are sent to your WoopSocial account through `api.woopsocial.com`, and media is uploaded to presigned URLs on `r2.cloudflarestorage.com`. WoopSocial then publishes to the social platforms you connected. Some skills can save files you approve, such as a content calendar CSV, to your working folder. See WoopSocial's [privacy policy](https://woopsocial.com/privacy-policy) and [terms of service](https://woopsocial.com/terms-of-service).

# Support

If you run into any issues, email us at `contact@woopsocial.com` or open an issue at [github.com/WoopSocial/mcp](https://github.com/WoopSocial/mcp/issues).
