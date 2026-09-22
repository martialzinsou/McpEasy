# 📚 Revolutionary Database Storage System - Wiki

## Table of Contents
- [Introduction](#introduction)
- [Quick Start](#quick-start)
- [Installation](#installation)
- [API Reference](#api-reference)
- [Usage Examples](#usage-examples)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Multi-language Support](#multi-language-support)

---

## Introduction

The **Revolutionary Database Storage System** is an intelligent, adaptive database platform that automatically:
- Deduplicates content using SHA-256 hashing
- Compresses large payloads with optimal ratios
- Learns from query patterns and suggests indexes
- Provides real-time analytics and optimization reports
- Supports multiple languages out-of-the-box

Built with **Flask** and **SQLAlchemy**, it provides a RESTful API for storing, searching, and optimizing data.

---

## Quick Start

### Prerequisites
- Python 3.8+
- PostgreSQL (preferred) or SQLite
- pip (Python package manager)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/revolutionary-db.git
cd revolutionary-db

# 2. Create a virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install flask flask-sqlalchemy

# 4. Set up database
# For PostgreSQL:
export DATABASE_URL="postgresql://user:password@localhost/revolutionary_db"

# For SQLite (default):
# No setup needed - will create revolutionary.db automatically

# 5. Run the application
python main.py
```

### First Run
The application will automatically:
- Create the database schema
- Initialize default adaptive patterns
- Start the HTTP server at `http://0.0.0.0:5000`

---

## API Reference

### Store Content Intelligently

```http
POST /api/v1/store
Content-Type: application/json

{
  "content": "Your data content here",
  "type": "document|image|log|video|audio|autre",
  "metadata": {
    "optional": "custom metadata"
  }
}
```

**Response:**
```json
{
  "status": "stored",
  "message": "Content stored with optimization",
  "record_id": 123,
  "data_hash": "sha256hashvalue",
  "content_type": "document",
  "compressed": false,
  "created_at": "2024-01-15T10:30:00"
}
```

**Status Values:**
- `stored`: New content was stored
- `duplicate`: Content already exists (deduplication working)

---

### Smart Pattern Search

```http
POST /api/v1/query-smart
Content-Type: application/json

{
  "pattern": "search term",
  "content_type": "document",  // optional
  "limit": 50  // optional, max 500
}
```

**Response:**
```json
{
  "results": [
    {
      "id": 1,
      "data_hash": "abc123...",
      "content_type": "document",
      "created_at": "2024-01-15T10:30:00",
      "metadata": {"key": "value"}
    }
  ],
  "total_found": 1,
  "pattern_searched": "search term",
  "suggestions": [
    {"pattern": "document", "usages": 45, "suggested": true}
  ]
}
```

---

### Storage Optimization Analysis

```http
POST /api/v1/optimize
Content-Type: application/json

{
  "table_name": "smart_records"
}
```

**Response:**
```json
{
  "summary": {
    "total_records": 15420,
    "unique_hashes": 13200,
    "deduplication_rate_percent": 85.62,
    "average_compression_ratio": 0.28,
    "optimization_score": 92.5
  },
  "type_distribution": {
    "document": 4500,
    "image": 3200,
    "log": 4500,
    "autre": 3220
  },
  "index_suggestions": [
    {
      "pattern": "search",
      "suggested_index": {"type": "fulltext", "columns": ["content_type", "metadata"]},
      "effectiveness": 0.85,
      "usages": 128
    }
  ],
  "recommendations": [
    {
      "priority": "high",
      "category": "deduplication",
      "message": "Consider increasing content retention period"
    }
  ]
}
```

---

### System Analytics

```http
GET /api/v1/analytics
```

**Response:**
```json
{
  "overview": {
    "total_records": 15420,
    "recent_activity_24h": 243,
    "total_unique_content": 13200
  },
  "by_type": {
    "document": 4500,
    "image": 3200,
    "log": 4500
  },
  "compression_metrics": {
    "total_compressed_blobs": 2840,
    "original_total_bytes": 52428800,
    "compressed_total_bytes": 15728640,
    "space_saved_bytes": 36700160,
    "space_saved_percent": 70.0
  },
  "query_patterns": {
    "total_tracked": 15,
    "high_usage_patterns": 8
  },
  "retrieved_at": "2024-01-15T10:30:00"
}
```

---

## Usage Examples

### Python Client

```python
import requests
import json

BASE_URL = "http://localhost:5000/api/v1"

# Store a document
response = requests.post(
    f"{BASE_URL}/store",
    json={"content": "Quarterly report Q3 2024", "type": "document"}
)
print(response.json())
# {'status': 'stored', 'record_id': 1, ...}

# Store the same content again (deduplication)
response = requests.post(
    f"{BASE_URL}/store",
    json={"content": "Quarterly report Q3 2024", "type": "document"}
)
print(response.json())
# {'status': 'duplicate', 'record_id': 1, ...}

# Search for content
response = requests.post(
    f"{BASE_URL}/query-smart",
    json={"pattern": "report"}
)
print(json.dumps(response.json(), indent=2))

# Get analytics
response = requests.get(f"{BASE_URL}/analytics")
print(json.dumps(response.json(), indent=2))
```

### cURL Examples

```bash
# Store content
curl -X POST -H "Content-Type: application/json" \
     -d '{"content": "Hello World", "type": "log"}' \
     http://localhost:5000/api/v1/store

# Smart query
curl -X POST -H "Content-Type: application/json" \
     -d '{"pattern": "Hello"}' \
     http://localhost:5000/api/v1/query-smart

# Optimization analysis
curl -X POST -H "Content-Type: application/json" \
     -d '{"table_name": "smart_records"}' \
     http://localhost:5000/api/v1/optimize

# Get analytics
curl http://localhost:5000/api/v1/analytics
```

### Multi-language Support

The system supports three languages out-of-the-box. To use a different language:

```python
# When making API calls, the system uses English by default
# but all status messages and documentation are available in:

# English (en) - default
# Spanish (es)  
# Russian (ru)

# Example with Spanish:
import requests
response = requests.post(
    "http://localhost:5000/api/v1/store",
    json={"content": "Hola mundo", "type": "document"}
)
# Status messages will be in the language configured
```

---

## Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `DATABASE_URL` | Database connection string | `sqlite:///revolutionary.db` |
| `FLASK_ENV` | Flask environment | `development` |
| `DEBUG` | Debug mode | `True` |

### Customizing Behavior

**Adjust compression threshold:**
```python
# In main.py, modify the needs_compression check:
needs_compression = len(content_bytes) > YOUR_THRESHOLD  # default: 10000 bytes
```

**Change default language:**
```python
# In main.py, modify create_app():
app = create_app(lang="es")  # 'en', 'es', or 'ru'
```

**Add custom adaptive patterns:**
```python
# In main.py, add to the initialization section:
custom_patterns = [
    AdaptiveIndex(
        query_pattern="custom_pattern",
        suggested_index={"type": "index", "columns": ["custom_field"]},
        usage_count=0,
        effectiveness_score=0.0,
    )
]
db.session.bulk_save_objects(custom_patterns)
db.session.commit()
```

---

## Troubleshooting

### Common Issues

**1. Database connection errors**
```
Error: SQLAlchemyError: Could not create engine from URL
```
**Solution:** Check `DATABASE_URL` environment variable format:
- PostgreSQL: `postgresql://user:password@host:port/dbname`
- MySQL: `mysql://user:password@host:port/dbname`
- SQLite: `sqlite:///path/to/database.db`

**2. Large payload errors**
```
Error: Request entity too large
```
**Solution:** Increase `MAX_CONTENT_LENGTH` in main.py or set environment variable:
```bash
export FLASK_MAX_CONTENT_LENGTH=50MB
```

**3. Performance degradation over time**
```
Warning: Query patterns not being tracked efficiently
```
**Solution:** The system automatically adapts, but you can help by:
- Making regular use of the `/api/v1/optimize` endpoint
- Ensuring query patterns are being used
- Checking the analytics endpoint for insights

**4. Language not displaying correctly**
```
Issue: Status messages in wrong language
```
**Solution:** Ensure `lang` parameter is set correctly in `create_app()`:
```python
app = create_app(lang="es")  # For Spanish
```

---

## Multi-language Support

The system includes built-in translation support for:

### English (`en`) - Default
- All API responses metadata
- Documentation strings
- Status messages

### Spanish (`es`)
- Full translation of application messages
- API endpoint descriptions
- Analytics labels

### Russian (`ru`)
- Cyrillic support for all text
- Technical terms translated
- Interface messages

**To add more languages:**
1. Add a new entry to the `TRANSLATIONS` dictionary in `main.py`
2. Use language code following ISO 639-1 format
3. All new keys will fallback to English if missing

**Language priority:**
1. `create_app(lang="xx")` parameter
2. `ACTIVE_LANG` config setting
3. Default to English (`en`)

---

## Contributing

### Adding Features
1. Fork the repository
2. Create a new branch: `git checkout -b feature/AmazingFeature`
3. Commit your changes
4. Push to the branch: `git push origin feature/AmazingFeature`
5. Open a Pull Request

### Improving Translations
1. Add or improve translations in the `TRANSLATIONS` dictionary
2. Test with `create_app(lang="your-language")`
3. Submit improvements via Pull Request

### Reporting Issues
- Use the GitHub Issues section
- Include error messages and steps to reproduce
- Mention your operating system and Python version

---

## License

This project is licensed under the **MIT License** - see the LICENSE file for details.

Copyright (c) 2024 Martial Zinsou

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.