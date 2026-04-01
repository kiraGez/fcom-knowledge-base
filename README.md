# FCOM Knowledge Base

An Electronic Flight Bag (EFB) style web application for searching and querying Flight Crew Operations Manuals (FCOMs) using AI-powered RAG (Retrieval Augmented Generation).

Built for [Puter.com](https://puter.com) - a privacy-first personal cloud platform.

## Features

- **EFB-Style Interface**: High-contrast dark theme matching real Electronic Flight Bag aesthetics
- **Multi-Aircraft Support**: Sidebar selection for B777, A320, B737 and FCOM/FCTM/QRH manuals
- **Admin Panel**: Hidden admin interface for PDF upload and processing (username-protected)
- **Section-Based Chunking**: Intelligent PDF parsing that detects section headers and chunks accordingly
- **Puter.kv Storage**: Global knowledge base stored in Puter's key-value store
- **AI-Powered Search**: RAG pipeline using Claude 3.5 Sonnet with context-aware responses
- **Citations**: AI responses include section/chapter citations

## Architecture

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   PDF Upload    │────▶│  Section Parser  │────▶│   Puter.kv      │
│   (Admin Only)  │     │   (PDF.js)       │     │   Storage       │
└─────────────────┘     └──────────────────┘     └─────────────────┘
                                                          │
┌─────────────────┐     ┌──────────────────┐             │
│  User Query     │────▶│  Keyword Search  │◀────────────┘
│                 │     │  (Top 5 chunks)  │
└─────────────────┘     └──────────────────┘
                               │
                               ▼
                        ┌──────────────────┐
                        │  Claude 3.5      │
                        │  Sonnet API      │
                        └──────────────────┘
                               │
                               ▼
                        ┌──────────────────┐
                        │  Cited Answer    │
                        │  + Source Links  │
                        └──────────────────┘
```

## Tech Stack

- **Frontend**: HTML5, Tailwind CSS (CDN)
- **PDF Parsing**: PDF.js 3.11.174
- **Backend/Storage**: Puter.com (Puter.kv, Puter.ai)
- **AI Model**: Claude 3.5 Sonnet (via Puter.ai)

## Deployment

1. Log in to [Puter.com](https://puter.com)
2. Create a new app/site
3. Upload `index.html`
4. Access the Admin Panel (requires configured username)
5. Upload and process your FCOM PDFs

## Admin Access

Admin panel is visible only when logged in with the configured admin username. Edit `ADMIN_USERNAME` in `index.html` to set your admin user.

## Data Structure

Documents are stored in Puter.kv under the key `fcom_knowledge_base`:

```json
{
  "B777": {
    "FCOM": [
      {
        "title": "Section Title",
        "text": "Section content...",
        "startPage": 42,
        "aircraft": "B777",
        "manual": "FCOM"
      }
    ]
  }
}
```

## License

MIT
