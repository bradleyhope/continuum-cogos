# COGOS - Continuum Operations System

**Continuum Capital Media Intelligence & Operations Tracking**

## Overview

COGOS (Continuum Operations System) is the central repository for tracking media monitoring operations, intelligence gathering, and analytical deliverables for Continuum Capital's portfolio monitoring activities.

## Purpose

- **Centralized Intelligence**: Track all media mentions, sentiment analysis, and coverage trends
- **Operational History**: Maintain complete records of monitoring sessions and deliverables
- **Data Repository**: Store curated article databases with AI-generated sentiment scores
- **Reporting Framework**: Templates and tools for generating professional weekly media reviews

## Structure

```
continuum-cogos/
├── subjects/              # Individual subject monitoring
│   └── lars-windhorst/   # Lars Windhorst media tracking
│       ├── articles/     # Curated article database
│       ├── reports/      # Weekly media reviews (PDF/MD)
│       ├── data/         # Raw data and sentiment scores
│       └── sessions/     # Session logs and notes
├── templates/            # Report templates and frameworks
├── tools/               # Monitoring and analysis tools
└── docs/                # Documentation and guides
```

## Current Subjects

### Lars Windhorst
- **Status**: Active monitoring
- **Articles Collected**: 82+ with AI sentiment analysis
- **Coverage Period**: 2015-2025
- **Key Themes**: Tennor Holding bankruptcy, H2O scandal, FSG shipyards, Hertha BSC, legal issues
- **Sources**: Financial Times, Bloomberg, WSJ, Reuters, Handelsblatt, L'Agefi

## Deliverables

### Media Monitoring Platform
- Full-stack web application with automated news tracking
- Real-time dashboard with coverage momentum indicators
- AI-powered sentiment analysis (OpenAI)
- Author tracking and journalist analytics
- PDF report generation with Continuum branding

### Article Database
- 82 articles with sentiment scores (-1.00 to 1.00)
- Multi-language coverage (English, German, French)
- Comprehensive metadata (source, author, date, topics)
- Historical coverage from 2015-2025

### Weekly Media Reviews
- Professional PDF reports in Continuum Capital style
- Executive summaries with key developments
- Detailed analysis with citations
- Trend tracking and sentiment analysis

## Technology Stack

- **Frontend**: React 19, Tailwind CSS 4, shadcn/ui
- **Backend**: Node.js, Express, tRPC
- **Database**: MySQL/TiDB with Drizzle ORM
- **AI/ML**: OpenAI GPT-4 for sentiment analysis
- **APIs**: NewsAPI, Google Custom Search, OpenAI
- **Monitoring**: Automated 6-hour interval checks

## Getting Started

See individual subject directories for specific monitoring details and data.

## Contact

Continuum Capital Operations
Powered by Manus AI

---

**Last Updated**: January 16, 2026
