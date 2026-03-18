# Sentinel System Architecture

## Data Flow

User searches topic on frontend
Frontend calls /api/analyze/{topic} on backend
Backend queries Qdrant for 15 most similar article vectors
Qdrant returns semantically matched articles
Backend sends articles to Featherless Mistral-7B for analysis
AI returns structured threat assessment JSON
Backend returns complete analysis to frontend
Frontend renders risk score, narratives, network graph

## Data Refresh Flow

Apify RSS Feed Aggregator runs on schedule
Collects articles from 12 news sources as JSON
Backend /api/refresh endpoint fetches from Apify dataset
sentence-transformers converts each article to 384-dim vector
Vectors and metadata stored in Qdrant collection
Frontend displays updated article count automatically

## Component Diagram

Apify Platform feeds into Backend API
Backend API connects to Qdrant Cloud
Backend API connects to Featherless AI
Backend API serves Frontend Dashboard
Frontend Dashboard displays Live Feed, Network Graph, Threat Assessment
