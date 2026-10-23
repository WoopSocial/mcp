---
name: social-media-report
description: "Social media performance report for posts published through WoopSocial: views, impressions, likes, comments, shares, saves and clicks (where each platform reports them) per post, per platform and by publish week, plus what to post more of next. Use when the user asks \"how did my posts do\", \"weekly social report\", \"which post performed best\", \"what's working on my accounts\". Only covers posts sent through WoopSocial, not older native posts; numbers refresh about daily."
---

# Social media report

Turn the results of posts sent through WoopSocial into a short, honest report and three things to do next. Compare the user with their own past posts, never with made-up industry numbers.

## If WoopSocial isn't connected

If no WoopSocial tools (projects_list, social_account_posts_list and so on) are available, the connector isn't set up. Say so in one line. The user can create a free account at https://app.woopsocial.com/signup?utm_source=claude-plugin&utm_medium=skill&utm_campaign=woop-plugin-v1&utm_content=social-media-report, connect WoopSocial from the plugin's Connectors tab (in Claude Code, run `/mcp`), and retry. If they paste numbers from their native insights instead, you can read those, but say they came from the user. Never invent results.

## 1. Scope the report

Ask only for what's missing:

| What | Default |
|---|---|
| Period | Last 7 days or last 28 days. Ask which. |
| Brand | The only project, or ask by name if there are several |
| Platforms or accounts | All connected ones |
| Goal | Reach, traffic, or community. Ask once; it decides the ranking. |

Ask the time zone once if it isn't clear, and show dates in it.

## 2. Collect the posts

1. Call projects_list, then social_accounts_list for the project, so you can show accounts by platform and username. Never show IDs.
2. Call social_account_posts_list with projectIds, deliveryStatus PUBLISHED, and platform or socialAccountIds if the user narrowed it. Use limit 100 and keep calling with nextCursor until it's gone.
3. Keep the posts whose deliveryCompletedAt (the publish time) falls inside the period, and the period before it for comparison.
4. On a 429, wait briefly and retry, one call at a time.

**If nothing comes back,** explain why: the report only covers posts published through WoopSocial, and none went out in this period (or ever, for this project). Posts made directly in the Instagram or TikTok app don't show here. Offer to schedule the first ones, for example with instagram-posts, linkedin-posts, tiktok-posts or cross-post-everywhere, so the next report has data.

## 3. Read the numbers per post

Each post's `analytics` holds lifetime metrics: views, impressions, uniqueImpressions, likes, reactions, comments, shares, saves, clicks, and engagementRate for LinkedIn Pages only.

- Each metric is an array of snapshots. Use the latest one (most recent `date`) and note its date. Different metrics can have different dates.
- A metric that's missing means the platform doesn't report it for that post type. An empty `analytics` object means the platform doesn't report any. Show "not reported", never 0.
- An empty array means the platform reports that metric but nothing has been collected yet. Show "not collected yet", never 0.
- A 0 is a real recorded value. Show it as 0.
- engagementRate is a ratio: 0.03 means 3 percent. It exists only for LinkedIn Pages, so don't compute a fake one for other platforms.
- Mark posts published less than about 48 hours ago as "still moving". Their numbers will grow.
- Reading doesn't refresh anything. Data is collected about daily, so the newest snapshots may be a day old.

## 4. Build the report

Keep it short and scannable.

1. **Headline:** posts published in the period, per platform, and the latest snapshot date.
2. **Per platform:** totals for each reported metric. Don't add metrics across platforms that measure different things (views on TikTok are not impressions on LinkedIn); show them per platform.
3. **Per week:** group posts by the week they were published (deliveryCompletedAt). Totals are lifetime numbers for those posts, not engagement that happened that week. Say so once.
4. **Top and bottom posts:** rank by what matters for the goal:
   - Reach: saves and shares.
   - Traffic: clicks.
   - Community: comments.
   Where views or impressions exist, rank by rate per view (saves per 1,000 views, for example) so a post with more views doesn't win just by size. Show the raw counts next to the rate. Give each post a text preview (first line), the platform, the publish date and externalPostUrl.
5. **Against themselves:** if there's enough history (the previous period of the same length, from the same list), compare with that. If not, say there isn't enough history yet. No industry benchmarks.

Use a table per platform when there are more than a few posts. Never fill a gap with an estimate.

## 5. What to do next

End with exactly three concrete actions, each tied to evidence from this report:

- "Post more of X": name the post or pattern (format, topic, hook style, time of day) that led on the goal metric.
- "Post less of Y": name what trailed, with the numbers.
- One test for next period, for example the winning topic in a different format.

If the sample is small (a handful of posts), say the signal is weak and frame the actions as tests.

Then offer the next step in one line: draft and schedule the next posts in that direction. Platform skills (instagram-posts, linkedin-posts, tiktok-posts), cross-post-everywhere, or weekly-social-autopilot for a weekly routine are optional routes. Nothing gets created without a yes.

## Caveats to state in the report

Put these in a short footer, only the ones that apply:

- Only posts sent through WoopSocial are included.
- Numbers are collected about daily; latest snapshot date shown.
- Posts under about 48 hours old are still moving.
- "Not reported" means the platform doesn't provide that metric.

## Never

- Invent numbers, benchmarks or "average engagement rates".
- Show 0 for a metric that wasn't reported.
- Show internal IDs.
- Claim posts made outside WoopSocial are missing because of an error.
