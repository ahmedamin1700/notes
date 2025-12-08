---
id: 06119643-0167-4e34-9f8a-b13de79aa585
aliases:
  - caching-moching
tags: []
---

# caching-moching

## 1. Caching (The "Don't Repeat Yourself" of Data)
APIs have rate limits (e.g., 60 calls/minute). If you run your script 100 times, you get blocked.
**Solution:** Save the result locally with a timestamp.

**Logic:**
1. User asks for "Cairo".
2. Check `cache.json`.
   - Is "Cairo" there?
   - Is the data less than 10 minutes old?
   - **YES:** Return saved data (Fast! No Internet!)
   - **NO:** Call API -> Save result to `cache.json` -> Return data.

## 2. Mocking (Testing without Internet)
You cannot rely on real APIs for unit tests because:
- The internet might be down.
- The API might change.
- You have a usage limit.

We use a library called `responses` or `unittest.mock` to **fake** the API.

**Example with `responses` library:**
```python
import responses
import requests

@responses.activate
def test_get_weather():
    # 1. Tell Python: "If anyone calls this URL, give them THIS JSON"
    responses.add(
        responses.GET,
        "https://api.openweathermap.org/data/2.5/weather",
        json={"main": {"temp": 20}, "weather": [{"description": "sunny"}]},
        status=200
    )

    # 2. Run your ACTUAL function
    client = WeatherClient()
    data = client.get_weather("London")

    # 3. Assert
    assert data["main"]["temp"] == 20
    # The real internet was NEVER touched!
```