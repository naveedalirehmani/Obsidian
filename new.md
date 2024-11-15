# News Aggregator App

  

Welcome to the News Aggregator App! This project is designed as a take-home challenge for the Frontend web developer position. The goal is to build a user-friendly interface that aggregates news articles from multiple sources and presents them in a clean, accessible format.

  

## Project Overview

  

The News Aggregator App allows users to:

  

1. **Search and Filter Articles**: Users can search for articles by keyword and filter results by date, category, and source.

2. **Personalize News Feed**: Users can customize their news feed by selecting their preferred sources, categories, and authors.

3. **Mobile-Responsive Design**: The application is optimized for viewing on mobile devices.

  

### Data Sources

  

This app uses the following data sources to fetch articles:

  

- **NewsAPI**: Provides access to articles from various news sources including major newspapers, magazines, and blogs.

- **The Guardian**: Accesses articles from The Guardian newspaper.

- **New York Times**: Fetches articles from The New York Times.

  

## Technologies Used

  

- **Frontend**: React.js

- **Containerization**: Docker

- **APIs**: NewsAPI, The Guardian API, New York Times API

  

## Getting Started

  

### Prerequisites

  

- Docker: Ensure you have Docker installed on your machine. You can download it from [Docker's official website](https://www.docker.com/get-started).

  

### Setting Up Environment Variables

  

Update your `docker-compose.yml` file with the following environment variables:

  

```yaml

REACT_APP_NEWS_API: "your_newsapi_key"

REACT_APP_THE_GUARDIAN: "your_guardian_api_key"

REACT_APP_NY_TIMES: "your_nytimes_api_key"

```

  
