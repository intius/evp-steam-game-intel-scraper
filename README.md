# Steam Game Scraper & Unofficial API (Python, Node.js, MCP)

[Run Steam Game Intelligence Scraper - Owners, Players & Pricing on Apify](https://apify.com/evpp/steam-game-intel) to export Steam Game data as clean JSON, CSV, Excel, or an API feed. This repository is a developer quick-start kit with working Python and Node.js clients, an MCP configuration, a real sample dataset, and an n8n automation template.

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-orange)](https://apify.com/evpp/steam-game-intel)

[Open the documentation and crawlable sample explorer](https://intius.github.io/evp-labs-data-extractors/actors/steam-game-intel/) for quick inputs, integration links, real sample rows, and ready-made task examples.

## Why use this Steam Game scraper?

- Export Steam Game data without building or maintaining a custom scraper
- Get flat, schema documented JSON ready for analytics, lead generation, market research, and AI agents
- Run manually, on a schedule, through the Apify API, or through MCP compatible AI tools
- Use the included 25+ row sample dataset to prototype before running the live Actor

Built for Indie game studios doing market research, game publishers/investors sizing genres, analysts tracking competitor pricing.

## Quick start on Apify

Open [https://apify.com/evpp/steam-game-intel](https://apify.com/evpp/steam-game-intel) and use this input:

```json
{
  "topList": "top100in2weeks",
  "includeSteamSpy": true,
  "includeReviews": true,
  "maxItems": 10
}
```

## Python

```bash
pip install -r requirements.txt
export APIFY_TOKEN=your_apify_token
python python/run.py
```

On Windows PowerShell, use `$env:APIFY_TOKEN="your_apify_token"` instead of `export`.

## Node.js

```bash
npm install
export APIFY_TOKEN=your_apify_token
node node/run.mjs
```

## MCP and AI agents

Add the hosted Apify MCP server from `mcp-config.json` to your MCP client:

```json
{
  "mcpServers": {
    "apify": {
      "type": "http",
      "url": "https://mcp.apify.com/?tools=evpp/steam-game-intel"
    }
  }
}
```

Then ask your agent to run `evpp/steam-game-intel`, inspect the output schema, or export the latest dataset. The direct MCP URL is `https://mcp.apify.com/?tools=evpp/steam-game-intel`.

## n8n automation

Import `n8n-workflow.json` into n8n, select your Apify credential, replace the webhook placeholder, and activate the schedule. The workflow runs the Actor every morning and posts fresh dataset items to your webhook.

## Output schema

| Field | Type | Description |
|---|---|---|
| `appId` | integer | Steam application ID |
| `name` | string | Game title |
| `url` | string | Steam store page URL |
| `type` | string | Steam app type (game, dlc, demo, music, ...) |
| `developer` | string | Primary developer |
| `publisher` | string | Primary publisher |
| `isFree` | boolean | Whether the game is free to play |
| `price` | number | Current price in major currency units (USD) |
| `currency` | string | ISO currency code of the price |
| `discountPercent` | integer | Active discount percentage (0 = no discount) |
| `releaseDate` | string | Release date (ISO YYYY-MM-DD when parsable) |
| `comingSoon` | boolean | Whether the game is not released yet |
| `genres` | string[] | Steam store genres |
| `platforms` | string[] | Supported platforms (windows, mac, linux) |
| `owners` | string | SteamSpy estimated owners range |
| `positive` | integer | SteamSpy positive review count |
| `negative` | integer | SteamSpy negative review count |
| `userScore` | integer | SteamSpy user score (0-100 percentage of positive reviews) |
| `scoreRank` | integer | SteamSpy score rank position |
| `ccu` | integer | Concurrent players right now (SteamSpy estimate) |
| `reviewScore` | string | Steam review score label (e.g. Very Positive). Derived from the SteamSpy user score when the reviews endpoint is unreachable. |
| `totalPositive` | integer | Total positive reviews (Steam reviews endpoint, SteamSpy fallback) |
| `totalNegative` | integer | Total negative reviews (Steam reviews endpoint, SteamSpy fallback) |
| `recommendations` | integer | Total Steam user recommendations/reviews as reported by the store API |

## Real sample output

The first sanitized row from the included sample dataset:

```json
{
  "appId": 10,
  "name": "Counter-Strike",
  "url": "https://store.steampowered.com/app/10/",
  "type": "game",
  "developer": "Valve",
  "publisher": "Valve",
  "isFree": false,
  "price": 9.99,
  "currency": "USD",
  "discountPercent": 0,
  "releaseDate": "2000-11-01",
  "comingSoon": false,
  "genres": [
    "Action"
  ],
  "platforms": [
    "windows",
    "mac",
    "linux"
  ],
  "owners": "20,000,000 .. 50,000,000",
  "positive": 165704,
  "negative": 5175,
  "userScore": 96,
  "scoreRank": 99,
  "ccu": 11366,
  "reviewScore": "Overwhelmingly Positive",
  "totalPositive": 165704,
  "totalNegative": 5175,
  "recommendations": 170982
}
```

## Files in this kit

| File | Purpose |
|---|---|
| `python/run.py` | Working Python Apify API example |
| `node/run.mjs` | Working Node.js Apify API example |
| `mcp-config.json` | MCP server configuration for AI agents |
| `sample-output.json` | First five sanitized sample rows |
| `dataset-snapshot.csv` | 25+ row evaluation snapshot |
| `DATASET_CARD.md` | Dataset documentation and provenance |
| `n8n-workflow.json` | Scheduled n8n automation template |

## Fresh data

This repository contains a static evaluation sample. For current data, run the live Actor: https://apify.com/evpp/steam-game-intel

## Responsible use

The Actor reads public data from `store.steampowered.com`. Review the source site's terms and applicable privacy rules before production use.
