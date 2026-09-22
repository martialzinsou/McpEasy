# Revolutionary Database Storage System

**McpEasy** - A complete intelligent database storage system with adaptive indexing, automatic deduplication, and compression.

## 📖 Overview

A revolutionary database storage system that automatically:
- **Deduplicates** content using SHA-256 hashing
- **Compresses** large payloads with optimal ratios
- **Learns** from query patterns and suggests optimal indexes
- **Provides** real-time analytics and optimization reports
- **Supports** multiple languages out-of-the-box

Built with **Flask** and **SQLAlchemy**, providing a RESTful API for storing, searching, and optimizing data.

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/martialzinsou/McpEasy.git
cd McpEasy/revolutionary-db

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install flask flask-sqlalchemy

# Run the application
python main.py
```

The application will start at `http://localhost:5000` with these endpoints:
- `POST /api/v1/store` - Store content intelligently
- `POST /api/v1/query-smart` - Smart pattern search
- `POST /api/v1/optimize` - Storage optimization analysis
- `GET /api/v1/analytics` - System analytics

## 📚 Documentation

### Comprehensive Guides

- **[Wiki Usage Guide](https://github.com/martialzinsou/McpEasy/wiki)** - Complete user manual with installation, API examples, troubleshooting, and multi-language support
- **[API Reference](https://github.com/martialzinsou/McpEasy/wiki/API-Reference)** - Detailed endpoint documentation with request/response examples
- **[Configuration Guide](https://github.com/martialzinsou/McpEasy/wiki/Configuration)** - Environment variables, customization options, and troubleshooting

### Multi-language Support

The system supports 4 languages:
- **English** (`en`) - Default
- **Spanish** (`es`)
- **French** (`fr`)
- **Russian** (`ru`)

All interface messages, API responses, and documentation adapt automatically.

## 🛠️ Features

### Intelligent Storage
- Automatic deduplication preventing redundant storage
- Smart compression with ratio tracking
- Metadata enrichment with storage optimization flags

### Adaptive Indexing
- Pattern recognition from query history
- Automatic index suggestions
- Effectiveness scoring and tracking

### Analytics & Optimization
- Real-time storage metrics
- Space savings reporting
- Performance recommendations
- Query pattern analysis

### Developer Friendly
- RESTful JSON API
- Python client examples
- cURL examples
- Full source code with comments
- Database schema documented

## 📁 Project Structure

```
McpEasy/
├── revolutionary-db/          # Main application
│   ├── main.py               # Flask app with API (879 lines, fully commented)
│   ├── api/                  # API endpoints
│   ├── docs/                 # Technical documentation
│   ├── wiki/                 # User guide (462 lines, multilingual)
│   │   └── Usage-Guide.md
│   └── scripts/              # Utility scripts
├── README.md                 # Project overview (this file)
└── LICENSE                   # MIT License
```

## 💻 Usage Examples

### Python Client

```python
import requests

BASE_URL = "http://localhost:5000/api/v1"

# Store content
response = requests.post(
    f"{BASE_URL}/store",
    json={"content": "My data", "type": "document"}
)
print(response.json())
# {'status': 'stored', 'record_id': 1, ...}

# Search
response = requests.post(
    f"{BASE_URL}/query-smart",
    json={"pattern": "My"}
)

# Get analytics
response = requests.get(f"{BASE_URL}/analytics")
```

### cURL Commands

```bash
# Store content
curl -X POST -H "Content-Type: application/json" \
     -d '{"content": "test", "type": "log"}' \
     http://localhost:5000/api/v1/store

# Smart query
curl -X POST -H "Content-Type: application/json" \
     -d '{"pattern": "Hello"}' \
     http://localhost:5000/api/v1/query-smart

# Optimization
curl -X POST -H "Content-Type: application/json" \
     -d '{"table_name": "smart_records"}' \
     http://localhost:5000/api/v1/optimize

# Analytics
curl http://localhost:5000/api/v1/analytics
```

## 🔧 Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `DATABASE_URL` | Database connection | `sqlite:///revolutionary.db` |
| `FLASK_ENV` | Flask environment | `development` |
| `DEBUG` | Debug mode | `True` |

### Customizing

- **Compression threshold**: Modify `needs_compression` in `main.py` (default: 10KB)
- **Language**: Use `create_app(lang="es")` for Spanish, `"ru"` for Russian
- **Custom patterns**: Add adaptive indexing patterns in `create_app()` initialization

## 🛡️ License

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