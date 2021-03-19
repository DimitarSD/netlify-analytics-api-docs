# Top Locations

> To test the GET request an OAuth 2.0 token is required
>
> **GET Request URL:** `https://analytics.services.netlify.com/v1/[API_ID]/ranking/countries`

## Request

The countries endpoint request takes three parameters: `from`, `to`, and `timezone`.

- **from:** start of the period, represented in UNIX timestamp
- **to:** end of the period, represented in UNIX timestamp
- **timezone:** the timezone in which the date/time should be returned

The max available period for fetching analytics data is 30 days. Thus the `from` "oldest" value will always be `now minus 30d`

## Response

The countries endpoint response returns an object with two main properties `data` and `ingestion`.

The `data` property is a collection of objects. Each object has three properties `count`, `country_name` `resource`:

- **count:** number of requests to this resource
- **country_name:** name of the country
- **resource:** the ISO-3166 country code

The `ingestion` property contains general information like `status`, `ingestion_start`, `ingestion_end` where

- **ingestion_start:** the start date for the current analytics tracking. When Netlify started tracking analytics for your site.
- **ingestion_end:** the end date for the current analytics tracking. It's usually the date of the last full day.

```json
{
    "data": [
        {
            "count": 10,
            "country_name": "Italy",
            "resource": "IT"
        },
        {
            "count": 10,
            "country_name": "United States",
            "resource": "US"
        }
    ],
    "ingestion": {
        "status": "current",
        "ingestion_start": 1605186000000,
        "ingestion_end": 1616155200000
    }
}
```

**Example Request Parameters:**

```text
from=1615978719785
to=1616065119785
timezone=+0200
```
