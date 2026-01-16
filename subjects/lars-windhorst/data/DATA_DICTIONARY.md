# Lars Windhorst Article Database - Data Dictionary

**Last Updated**: January 16, 2026  
**Database Version**: 1.0  
**Total Articles**: 15

---

## Overview

This database contains curated media articles about Lars Windhorst with AI-generated sentiment analysis. Each article includes comprehensive metadata for tracking coverage trends, journalist patterns, and sentiment evolution over time.

---

## Schema

### Article Record Structure

```json
{
  "id": "string",
  "title": "string",
  "url": "string",
  "source": "string",
  "author": "string | null",
  "publishedAt": "YYYY-MM-DD",
  "language": "string",
  "description": "string",
  "sentiment": "positive | neutral | negative",
  "sentimentScore": "string (decimal -1.00 to 1.00)",
  "topics": ["string"],
  "keyEntities": ["string"]
}
```

---

## Field Definitions

### `id`
- **Type**: String
- **Required**: Yes
- **Unique**: Yes
- **Description**: Unique identifier for the article
- **Format**: Lowercase kebab-case, typically source-subject-topic-year
- **Example**: `"ft-windhorst-tennor-bankruptcy-2025"`

### `title`
- **Type**: String
- **Required**: Yes
- **Description**: Article headline/title
- **Language**: Original language of publication
- **Example**: `"Lars Windhorst's Tennor Holding declared bankrupt in Netherlands"`

### `url`
- **Type**: String (URL)
- **Required**: Yes
- **Unique**: Yes
- **Description**: Full URL to the original article
- **Example**: `"https://www.ft.com/content/tennor-holding-bankruptcy"`

### `source`
- **Type**: String
- **Required**: Yes
- **Description**: Publication name
- **Examples**: `"Financial Times"`, `"Handelsblatt"`, `"Bloomberg"`

### `author`
- **Type**: String or null
- **Required**: No
- **Description**: Article author name (null if not available)
- **Example**: `"Patrick Jenkins"` or `null`

### `publishedAt`
- **Type**: String (ISO 8601 date)
- **Required**: Yes
- **Format**: `YYYY-MM-DD`
- **Description**: Article publication date
- **Example**: `"2025-06-15"`

### `language`
- **Type**: String (ISO 639-1 code)
- **Required**: Yes
- **Description**: Article language
- **Values**: `"en"` (English), `"de"` (German), `"fr"` (French)
- **Example**: `"en"`

### `description`
- **Type**: String
- **Required**: Yes
- **Description**: Brief summary or excerpt of the article
- **Length**: Typically 100-300 characters
- **Example**: `"Dutch tax authorities initiate bankruptcy proceedings against Windhorst's primary investment vehicle over unpaid taxes"`

### `sentiment`
- **Type**: Enum String
- **Required**: Yes
- **Values**: `"positive"`, `"neutral"`, `"negative"`
- **Description**: Categorical sentiment classification
- **Methodology**: AI-generated based on title and description
- **Thresholds**:
  - `positive`: sentimentScore > 0.2
  - `neutral`: -0.2 ≤ sentimentScore ≤ 0.2
  - `negative`: sentimentScore < -0.2

### `sentimentScore`
- **Type**: String (decimal number)
- **Required**: Yes
- **Format**: Two decimal places (e.g., `"-0.95"`, `"0.70"`)
- **Range**: -1.00 (very negative) to 1.00 (very positive)
- **Description**: Quantitative sentiment score
- **Methodology**: OpenAI GPT-4 analysis considering:
  - Legal issues, bankruptcies, scandals → negative
  - Successful deals, investments → positive
  - Neutral reporting → neutral
- **Examples**:
  - `"-1.00"`: Arrest warrant issued
  - `"-0.85"`: Fraud indictment of successor
  - `"0.15"`: Neutral business update
  - `"0.70"`: Successful investment announcement

### `topics`
- **Type**: Array of Strings (stored as comma-separated in JSON string)
- **Required**: Yes
- **Description**: Thematic tags for categorization
- **Format**: Lowercase with underscores
- **Common Values**:
  - `"bankruptcy"`
  - `"tax_issues"`
  - `"h2o_scandal"`
  - `"hertha_bsc"`
  - `"fsg_shipyard"`
  - `"legal_issues"`
  - `"regulatory"`
  - `"real_estate"`
  - `"partnerships"`
- **Example**: `["bankruptcy", "tax_issues", "tennor_holding"]`

### `keyEntities`
- **Type**: Array of Strings
- **Required**: Yes
- **Description**: Named entities mentioned in the article
- **Format**: Proper case
- **Types**: People, organizations, locations
- **Example**: `["Lars Windhorst", "Tennor Holding B.V.", "Dutch Tax Authorities"]`

---

## Sentiment Scoring Methodology

### AI Analysis Process
1. **Input**: Article title + description
2. **Model**: OpenAI GPT-4-mini
3. **Prompt**: "Analyze sentiment about Lars Windhorst. Return number between -1 (very negative) and 1 (very positive). Consider legal issues, bankruptcies, scandals as negative; successful deals as positive."
4. **Output**: Decimal score rounded to 2 places

### Sentiment Guidelines
- **Highly Negative (-1.00 to -0.70)**: Arrest warrants, major bankruptcies, fraud charges
- **Moderately Negative (-0.69 to -0.40)**: Tax issues, insolvencies, legal disputes
- **Slightly Negative (-0.39 to -0.21)**: Minor setbacks, negative reporting
- **Neutral (-0.20 to 0.20)**: Factual reporting, business updates
- **Slightly Positive (0.21 to 0.40)**: Minor successes, neutral-positive news
- **Moderately Positive (0.41 to 0.70)**: Successful investments, partnerships
- **Highly Positive (0.71 to 1.00)**: Major deals, significant achievements

---

## Coverage Statistics

### By Source
- **Financial Times**: 3 articles (20%)
- **Handelsblatt**: 4 articles (27%)
- **Shippax**: 2 articles (13%)
- **Other**: 6 articles (40%)

### By Language
- **English**: 9 articles (60%)
- **German**: 6 articles (40%)

### By Sentiment
- **Negative**: 10 articles (67%)
- **Neutral**: 4 articles (27%)
- **Positive**: 1 article (6%)

### By Topic (Top 5)
1. **Legal Issues**: 7 articles
2. **Tax Issues**: 5 articles
3. **FSG Shipyard**: 4 articles
4. **H2O Scandal**: 3 articles
5. **Hertha BSC**: 2 articles

### Time Period
- **Earliest**: July 2020 (NY skyscraper investment)
- **Latest**: October 2025 (FSG shipyard takeover)
- **Peak Coverage**: 2024-2025 (bankruptcy, legal issues)

---

## Data Quality Notes

### Completeness
- All required fields populated
- Author field nullable (40% of articles have no author attribution)
- Some articles use aggregated sources (e.g., "MSN / German Press")

### Accuracy
- URLs verified as of database creation date
- Sentiment scores AI-generated, not manually validated
- Dates reflect publication date, not event date

### Limitations
- Database contains curated selection, not comprehensive coverage
- Sentiment analysis based on title/description only, not full article text
- Some paywalled articles may have limited description data

---

## Usage Examples

### Query by Sentiment
```javascript
// Get all negative articles
articles.filter(a => a.sentiment === "negative")

// Get highly negative articles
articles.filter(a => parseFloat(a.sentimentScore) < -0.70)
```

### Query by Topic
```javascript
// Get all bankruptcy-related articles
articles.filter(a => a.topics.includes("bankruptcy"))

// Get H2O scandal articles
articles.filter(a => a.topics.includes("h2o_scandal"))
```

### Query by Date Range
```javascript
// Get 2025 articles
articles.filter(a => a.publishedAt.startsWith("2025"))

// Get articles after June 2025
articles.filter(a => a.publishedAt >= "2025-06-01")
```

### Author Analytics
```javascript
// Get all Patrick Jenkins articles
articles.filter(a => a.author === "Patrick Jenkins")

// Calculate average sentiment by author
const byAuthor = articles.reduce((acc, a) => {
  if (!a.author) return acc;
  if (!acc[a.author]) acc[a.author] = [];
  acc[a.author].push(parseFloat(a.sentimentScore));
  return acc;
}, {});
```

---

## Maintenance

### Adding New Articles
1. Generate unique ID (source-subject-topic-year format)
2. Verify URL is accessible and unique
3. Run AI sentiment analysis on title + description
4. Classify sentiment category based on score
5. Add relevant topic tags
6. Extract key entities
7. Validate JSON structure

### Updating Existing Articles
- URLs should not change (use original URL)
- Sentiment scores may be recalculated if methodology improves
- Topics and entities can be refined for consistency

### Data Validation
- Check for duplicate URLs
- Verify date format (YYYY-MM-DD)
- Ensure sentiment score matches sentiment category
- Validate language codes (ISO 639-1)
- Check JSON syntax validity

---

## Related Files

- `articles-database.json` - Main article database
- `../reports/` - Generated weekly media reviews
- `../sessions/` - Session documentation and methodology
- `../../templates/weekly-media-review-template.md` - Report template

---

## Contact

For questions about data structure or methodology, refer to session documentation in `../sessions/`.
