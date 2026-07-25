# ⚡ Twitter (X) Comment Scraper

[![Apify Actor](https://img.shields.io/badge/Apify-Actor-orange?style=for-the-badge&logo=apify)](https://apify.com/mikolabs/twitter-comment-scraper)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9+-3776AB.svg?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![No Login Required](https://img.shields.io/badge/Auth-No%20Login%20/%20No%20API%20Key-brightgreen?style=for-the-badge)](#-why-choose-this-scraper)

> **Extract comments, replies, and engagement metrics from any X (Twitter) post at scale.**  
> **No login credentials, no API keys, no session cookies required.**

---

## 🔥 Why Choose This Scraper?

Extracting Twitter/X comments using official APIs or session-heavy scrapers is expensive, fragile, and rate-limited. This scraper solves all those pain points:

* 🔓 **Zero-Authentication**: No Twitter login, password, or developer API token needed.
* ⚡ **Ultra-Fast Performance**: Scrapes **20+ replies in under 2 seconds**.
* 💰 **Cost-Effective**: Highly optimized compute consumption — cost scales at **~$5.00 per 1,000 extracted results**.
* 🎯 **Smart Filters & Sorting**: Filter out low-quality comments by minimum likes and sort replies by **Relevance**, **Recency**, or **Likes**.
* 📊 **Rich Metadata**: Captures full user profiles (bio, followers, location, verification status), media attachments (images, video URLs), and post interaction metrics.
* 🛡️ **Built for Scale**: Cloud-ready on Apify with automatic retries and anti-blocking measures built-in.

---

## 💡 Key Use Cases

| Industry / Role | Use Case |
| :--- | :--- |
| **Growth & Lead Gen** | Find prospective buyers replying to competitor tweets or industry conversations. |
| **Sentiment Analysis** | Measure audience reactions to product launches, PR campaigns, or viral posts. |
| **Brand Protection** | Monitor replies on brand posts to catch negative feedback or support requests early. |
| **Influencer Vetting** | Analyze comment authenticity and sentiment before locking in influencer sponsorships. |
| **AI Data Training** | Gather high-quality public conversational data to train LLMs or sentiment classifiers. |

---

## 📊 Extracted Data Overview

Every scraped item returns comprehensive, structured JSON containing:

- **Reply Content**: Full text, language, timestamp, reply chain IDs, source app.
- **Engagement Metrics**: Likes, retweets, quotes, bookmarks, and view counts.
- **User / Author Profile**: Screen name, display name, user bio, follower/following counts, location, created date, verification status, and avatar URLs.
- **Media Attachments**: High-res image URLs, video streams, thumbnail URLs, and duration.

```json
{
  "id": "1815123456789012345",
  "text": "This feature saves so much time! Great work team 🚀",
  "createdAt": "Sun Jul 26 01:00:00 +0000 2026",
  "likeCount": 142,
  "retweetCount": 12,
  "replyCount": 3,
  "viewCount": 8500,
  "author": {
    "username": "tech_enthusiast",
    "name": "Jane Doe",
    "description": "Building cool stuff with Python & AI.",
    "followersCount": 12500,
    "isVerified": true,
    "profileImageUrl": "https://pbs.twimg.com/profile_images/..."
  },
  "media": []
}
```

---

## 🚀 Quick Start Guide

### Option 1: Run on Apify Cloud (Recommended)

1. Open the [Twitter (X) Comment Scraper on Apify](https://apify.com/mikolabs/twitter-comment-scraper).
2. Enter one or more **Tweet URLs**.
3. Choose your desired sorting option (**Relevance**, **Recency**, or **Likes**).
4. Hit **Start** and download your dataset as **JSON, CSV, or Excel**.

---

### Option 2: Run via Apify Python Client

```python
from apify_client import ApifyClient

# Initialize client with your Apify API token
client = ApifyClient("YOUR_APIFY_TOKEN")

# Prepare actor input
run_input = {
    "tweetUrls": [
        "https://x.com/elonmusk/status/1815000000000000000"
    ],
    "maxComments": 100,
    "sortBy": "relevance",
    "minLikes": 5
}

# Run the Actor and wait for it to finish
run = client.actor("mikolabs/twitter-comment-scraper").call(run_input=run_input)

# Fetch results from the dataset
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"[{item.get('author', {}).get('username')}]: {item.get('text')}")
```

---

### Option 3: Run via Node.js API Client

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({
    token: 'YOUR_APIFY_TOKEN',
});

const input = {
    tweetUrls: [
        'https://x.com/elonmusk/status/1815000000000000000'
    ],
    maxComments: 100,
    sortBy: 'likes'
};

(async () => {
    const run = await client.actor('mikolabs/twitter-comment-scraper').call(input);
    const { items } = await client.dataset(run.defaultDatasetId).listItems();
    console.log(`Fetched ${items.length} comments.`);
})();
```

---

## ⚙️ Configuration & Input Parameters

| Field | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `tweetUrls` | Array | *Required* | List of tweet / post URLs to extract comments from. |
| `maxComments` | Integer | `100` | Maximum number of comments to scrape per tweet URL. |
| `sortBy` | String | `"relevance"` | Order of replies: `relevance`, `recency`, or `likes`. |
| `minLikes` | Integer | `0` | Exclude comments with fewer than this number of likes. |
| `includeUserStats` | Boolean | `true` | Include detailed author profile metadata in the response. |

---

## ⚖️ Legal & Ethical Usage

This actor is designed for extracting publicly available comments and discourse on X (Twitter). Users are responsible for complying with relevant local regulations (e.g. GDPR, CCPA) regarding personal data processing and the platform's terms of service.

---

## 📞 Support & Custom Features

Need custom scrapers, bulk data feeds, or custom enterprise integrations?

* 🌐 **Apify Actor**: [Twitter Comment Scraper](https://apify.com/mikolabs/twitter-comment-scraper)
* 📬 **Issues & Requests**: Open an issue on this GitHub repository or contact via Apify support.

---

<p align="center">
Made with ❤️ by MikoLabs
</p>
