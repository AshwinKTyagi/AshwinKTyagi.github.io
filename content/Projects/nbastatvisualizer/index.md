---
title: "NBA Stat Visualizer"
summary: "A full-stack web app for visualizing NBA playoff brackets, head-to-head team matchups, and individual player stats using interactive charts."
date: 2025-04-01T00:00:00-00:00
aliases: ["/nbastatvisualizer"]
tags: ["Projects", "NBA Stat Visualizer"]
author: "Me"
showToc: true
TocOpen: false
draft: false
math: false
hidemeta: true
comments: false
description: "Duration: April 2025 - Current (WIP)"
canonicalURL: "https://canonical.url/to/Projects/nbastatvisualizer"
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: true
ShowReadingTime: false
ShowBreadCrumbs: false
ShowPostNavLinks: false
ShowWordCount: false
ShowRssButtonInSectionTermList: false
UseHugoToc: true
cover:
    image: "<image path/url>"
    alt: "<alt text>"
    caption: "<text>"
    relative: false
    hidden: true
editPost:
    URL: "https://github.com/AshwinKTyagi/AshwinKTyagi.github.io/tree/main/content"
    Text: "Suggest Changes"
    appendFilePath: true
---

### [Link to GitHub](https://github.com/AshwinKTyagi/NBA-Stat-Visualizer)

## Project Description

NBA Stat Visualizer is a full-stack application that brings NBA statistics to life through interactive visualizations. It features a playoff bracket explorer, head-to-head team matchup comparisons, and player stat radar charts — all powered by live data from NBA.com.

## Tech Stack

**Backend**
- FastAPI with CORS support
- `nba_api` for pulling live data from NBA.com
- `curl_cffi` for Chrome TLS impersonation to bypass bot detection
- Python virtual environment

**Frontend**
- React with TypeScript
- Vite (using the rolldown bundler)
- Recharts for data visualization
- Axios for API requests

## Features

### Playoff Bracket View

The home view displays the current playoff bracket with East and West conference seeds 1–8. Each first-round matchup is interactive, letting you drill into the head-to-head comparison for that series.

### Matchup Comparison

For any two teams, the app pulls their advanced stats and displays a side-by-side comparison with per-statistic advantage labels. This makes it easy to see where one team holds an edge over another going into a series.

### Player Radar Charts

Individual player stats are normalized to a 0–100 scale and rendered as radar charts. You can load up to two players simultaneously for a direct visual comparison across key categories like scoring, rebounding, assists, and efficiency.

### Team Advanced Stats

The backend fetches comprehensive per-team statistics from NBA.com, covering both traditional and advanced metrics. The season year is configurable via environment variable, so the app isn't hardcoded to any single season.

## Architecture

The backend exposes three routers mounted under `/api`:

- `/api/teams` — team stats and advanced metrics
- `/api/players` — individual player data and normalization
- `/api/matchups` — head-to-head matchup data

The frontend runs on port 5173 (Vite dev server) and connects to the backend on port 8000. TypeScript interfaces are centralized in a single definitions file to avoid import issues introduced by Vite's rolldown bundler.

One notable challenge was working around NBA.com's bot detection. The `curl_cffi` library handles this by impersonating a Chrome browser at the TLS level, which allows the `nba_api` requests to go through reliably.

## What's Next

This project is actively in development. Upcoming work includes:

- Expanding the bracket view to cover all rounds, not just the first round
- Adding historical season comparisons
- Improving the player search and selection flow
- Deploying the app so it's accessible without running locally
