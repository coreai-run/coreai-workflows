---
name: workflow:news
type: pipeline
description: Aggregate news from multiple sources. USE WHEN user says 'radar', 'news', 'noticias', 'trending', 'news digest', 'what's happening'.
---

# News Pipeline

Aggregates news from multiple sources into a unified digest.

## Configuration
!`coreai config show news`

## Active Profile
Using configuration from: !`coreai profile current`

## Overview

This pipeline fetches news from multiple sources and creates a deduplicated, prioritized digest.

## Steps

### 1. Reddit
Read and execute: `~/.coreai/skills/reddit-reader/SKILL.md`

**Input**: Configuration from `reddit-reader`
**Output**: List of Reddit posts with scores

### 2. Hacker News
Read and execute: `~/.coreai/skills/hackernews-reader/SKILL.md`

**Input**: Configuration from `hackernews-reader`
**Output**: List of HN stories with points

### 3. GitHub Trending
Read and execute: `~/.coreai/skills/github-reader/SKILL.md`

**Input**: Configuration from `github-reader`
**Output**: List of trending repos with stars

### 4. RSS Feeds
Read and execute: `~/.coreai/skills/rss-reader/SKILL.md`

**Input**: Configuration from `rss-reader`
**Output**: List of RSS articles

### 5. YouTube (Optional)
If `YOUTUBE_API_KEY` is set:
Read and execute: `~/.coreai/skills/youtube-reader/SKILL.md`

### 6. Gmail (Optional)
If Gmail OAuth is configured:
Read and execute: `~/.coreai/skills/inbox-reader/SKILL.md`

## Post-Processing

After collecting from all sources:

1. **Deduplicate**
   - Remove duplicate URLs
   - Merge similar titles (if `dedupe.by: title_similarity`)

2. **Prioritize**
   - Sort by engagement (score/stars/points)
   - Boost recent items

3. **Format**
   - Group by source type
   - Limit to `max_items_per_source`
   - Add summary section

## Output Format

## News Digest - {date}

### Summary
Found {total} items from {sources} sources in the last {hours} hours.

### Reddit ({count})
- [Title](url) - r/subreddit - 523 pts

### Hacker News ({count})
- [Title](url) - 234 pts, 45 comments

### GitHub ({count})
- [owner/repo](url) - 1,234 stars

### RSS ({count})
- [Title](url) - Source - 2h ago

---
*Generated at {timestamp}*

## Error Handling

If any reader fails:
1. Log the error
2. Continue with remaining readers (if `continue_on_error: true`)
3. Note skipped sources in output

## Execution Instructions

1. Execute each reader skill in order
2. Collect all results into a unified list
3. Apply deduplication
4. Apply prioritization
5. Format final output
6. Present to user
