---
name: news-aggregator-skill
description: Comprehensive news aggregator that fetches, filters, and deeply analyzes real-time content from 8 major sources: Hacker News, GitHub Trending, Product Hunt, 36Kr, Tencent News, WallStreetCN, V2EX, and Weibo. Best for 'daily scans', 'tech news briefings', 'finance updates', and 'deep interpretations' of hot topics.
---

# News Aggregator Skill

Fetch real-time hot news from multiple sources.

## Tools

### fetch_news.py

**Usage:**

```bash
### Single Source (Limit 10)
```bash
python3 scripts/fetch_news.py --source hackernews --limit 10 --deep
```

### Global Scan (All Sources)
```bash
python3 scripts/fetch_news.py --source all --limit 10 --keyword "AI" --deep
``````

**Arguments:**

- `--source`: One of `hackernews`, `weibo`, `github`, `36kr`, `producthunt`, `v2ex`, `tencent`, `wallstreetcn`, `all`.
- `--limit`: Max items per source (default 10).
- `--keyword`: Comma-separated filters (e.g. "AI,GPT").
- `--deep`: **[NEW]** Enable deep fetching. Downloads and extracts the main text content of the articles.

**Output:**
JSON array. If `--deep` is used, items will contain a `content` field associated with the article text.

## Interactive Menu

When the user says **"news-aggregator-skill 如意如意"** (or similar "menu/help" triggers):
1.  **READ** the content of `templates.md` in the skill directory.
2.  **DISPLAY** the list of available commands to the user exactly as they appear in the file.
3.  **GUIDE** the user to select a number or copy the command to execute.

## Response Guidelines (CRITICAL)

When presenting the results to the user, you **MUST** follow these rules:

1.  **Language**: Always translate the summary and insights into **Chinese (Simplified)**, even if the source is English.
2.  **Format**: Use a polished, magazine-style format.
3.  **Deep Analysis**: For items with `content` (Deep Fetch), you **MUST** provide the following section for **EVERY item regardless of domain** (Tech, Finance, etc.):
    *   **Structure**:
        *   **Title**: Translate to Chinese found suitable. **MUST be a Markdown Link** pointing to the `url`.
        *   **Metadata**: Source, Publish Time (发布时间), Heat (热度).
        *   **One-liner**: A catchy, single-sentence summary (一句话介绍).
        *   **Deep Interpretation**: Bullet points explaining *why* this matters, technical details, or background context.

**Example Output Format:**

```markdown
### 📰 Hacker News 今日精选深度解析

> **数据来源**: Hacker News (Top 5)
> **生成时间**: 2026-01-18

#### 1. 🛠️ [Iconify：开源图标库的终极聚合方案](https://icon-sets.iconify.design/)
*   **原文标题**: Iconify: Library of Open Source Icons
*   **发布时间**: 6 hours ago
*   **热度**: 🔥 318 points
*   **一句话介绍**: 前端开发的福音，一个接口搞定所有图标库。
*   **深度解读**:
    Iconify 不仅仅是一个图标包，它是一个 **统一的图标框架**...


4.  **Archiving**: Save the final report to the `reports/` directory with a timestamped filename (e.g., `reports/hn_news_YYYYMMDD_HHMM.md`) to maintain a history.
5.  **Full Rendering**: Always output the **ENTIRE** content of the report in the chat conversation. Do not just say "Report generated", show the full markdown.

