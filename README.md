# News Feed Aggregator

A custom ChatGPT action that fetches and aggregates news from multiple RSS feeds, organized by category. The action pulls content from Reddit, New York Times, and ESPN sources to provide a comprehensive news summary.

## Categories

- **Local News**: Melbourne and Australian news from Reddit
- **Tech News**: Updates from ChatGPT, Claude AI, cybersecurity, and technology subreddits, plus NYT tech coverage
- **World News**: International coverage from NYT, with focus on World and Asia Pacific
- **Sports News**: Basketball coverage from NYT and cricket updates from ESPN
- **Opinions**: Columns from NYT writers including Bret Stephens, Ezra Klein, Paul Krugman, and Nicholas Kristof

## API Endpoint

The API provides a single endpoint `/fetchFeeds` that accepts the following parameters:

- `categories` (optional): Comma-separated list of categories to fetch (local, tech, world, sports, opinions)
- `hours` (optional): Only return articles from the past X hours (default: 24, max: 168)
- `limit` (optional): Maximum number of articles per feed (default: 5, max: 20)

### Example Usage

```javascript
// Fetch all categories from last 24 hours
GET /fetchFeeds

// Fetch tech news from last 12 hours
GET /fetchFeeds?categories=tech&hours=12

// Fetch local and world news, limited to 10 articles per feed
GET /fetchFeeds?categories=local,world&limit=10
```

### Response Format

The API returns JSON with:
- Current timestamp
- Time filter details
- Categories with their respective feeds
- Articles from each feed matching the time and limit criteria

## RSS Sources

### Local News
- Reddit Melbourne: `https://www.reddit.com/r/Melbourne/.rss`
- Reddit Australia: `https://www.reddit.com/r/Australia/.rss`

### Tech News
- Reddit ChatGPT: `https://www.reddit.com/r/ChatGPT/.rss`
- Reddit ClaudeAI: `https://www.reddit.com/r/ClaudeAI/.rss`
- Reddit Cybersecurity: `https://www.reddit.com/r/cybersecurity/.rss`
- Reddit Technology: `https://www.reddit.com/r/technology/.rss`
- NYT Technology: `https://rss.nytimes.com/services/xml/rss/nyt/Technology.xml`
- Reddit Line6 Helix: `https://www.reddit.com/r/Line6Helix/.rss`
- NYT Personal Tech: `https://rss.nytimes.com/services/xml/rss/nyt/PersonalTech.xml`

### World News
- NYT World News: `https://rss.nytimes.com/services/xml/rss/nyt/World.xml`
- NYT Asia Pacific: `https://rss.nytimes.com/services/xml/rss/nyt/AsiaPacific.xml`

### Sports News
- NYT Pro Basketball: `https://rss.nytimes.com/services/xml/rss/nyt/ProBasketball.xml`
- ESPN Cricinfo: `https://www.espncricinfo.com/rss/content/story/feeds/2.xml`

### Opinions
- NYT Bret Stephens: `https://www.nytimes.com/svc/collections/v1/publish/www.nytimes.com/column/bret-stephens/rss.xml`
- NYT Ezra Klein: `https://www.nytimes.com/svc/collections/v1/publish/www.nytimes.com/column/ezra-klein/rss.xml`
- NYT Paul Krugman: `https://www.nytimes.com/svc/collections/v1/publish/www.nytimes.com/column/paul-krugman/rss.xml`
- NYT Nicholas Kristof: `https://www.nytimes.com/svc/collections/v1/publish/www.nytimes.com/column/nicholas-kristof/rss.xml`

## Error Handling

The API includes standard error responses:
- `400`: Invalid request parameters
- `429`: Too many requests to RSS feeds
- `500`: Error fetching RSS feeds

## Usage Notes

- Time filtering defaults to the last 24 hours but can be extended up to one week
- Articles are ordered by publication date
- Each feed is limited to prevent overwhelming responses
- The API respects rate limits of the underlying RSS feeds

## Setup

1. Save the OpenAPI specification as `news-feeds.json`
2. Create a new ChatGPT custom action
3. Import the specification file
4. Use the action to fetch and summarize news based on your preferences
