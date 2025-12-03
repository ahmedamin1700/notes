---
id: fdaf2581-fb77-44e4-b9c8-ddf9ea3d0aff
aliases:
  - http-apis-secrets
tags: []
---

# http-apis-secrets
## Week 3: HTTP, APIs & Secrets

## 1. HTTP Requests (The Language of the Web)
Python doesn't "open websites" like a browser. It sends **HTTP Requests**.
We use the `requests` library (industry standard).

- **GET**: "Give me data" (e.g., Check weather).
- **POST**: "Here is data, save it" (e.g., Submit a form).
- **Status Codes**:
    - `200 OK`: Success.
    - `401 Unauthorized`: You didn't provide a valid API Key.
    - `404 Not Found`: The city/URL doesn't exist.
    - `500 Server Error`: The API server crashed.

## 2. Query Parameters
URLs look like this: `https://api.weather.com/v1/current?city=Cairo&units=metric`
- Everything after `?` are parameters.
- `city=Cairo`
- `units=metric`
In `requests`, we pass these as a Python dictionary: `params={"city": "Cairo"}`.

## 3. API Keys & Security (CRITICAL)
APIs are not free. Services give you a "Key" (like a password).
**NEVER commit API keys to GitHub.** Bots scan GitHub in seconds and will steal them.

### The Solution: Environment Variables (`.env`)
1. We create a file named `.env` locally (contains the secret).
2. We add `.env` to `.gitignore` (so it never goes to GitHub).
3. We use `python-dotenv` to read the file in Python.

**Example `.env` file:**
```text
WEATHER_API_KEY=12345secret
Example Python usage:
code
Python
import os
from dotenv import load_dotenv

load_dotenv() # Loads the .env file
api_key = os.getenv("WEATHER_API_KEY") # Safely grabs the string
```

## 4. JSON Responses
APIs return data as JSON strings. requests converts this to a Python Dictionary automatically using .json().

```Python
response = requests.get(url)
data = response.json()
# data is now {'temp': 20, 'city': 'Cairo'}
```

**Folder Structure:**
```text
python-job-ready/
├── weather_cli/           (New Project)
│   ├── __init__.py
│   ├── main.py            (CLI Entry Point)
│   ├── api_clients.py     (Where the logic lives)
│   └── tests/
├── .env                   (Your secrets - NOT in git)
├── .gitignore             (Update to ignore .env)
└── pyproject.toml         (Managed by uv)