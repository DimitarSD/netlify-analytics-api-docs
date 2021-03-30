# Top Pages

> To test the GET request an OAuth 2.0 token is required
>
> **GET Request URL:** `https://analytics.services.netlify.com/v1/[API_ID]/ranking/pages`

## Request

The pages endpoint request takes four parameters: `from`, `to`, `timezone`, and `limit`.

- **from:** start of the period, represented in UNIX timestamp
- **to:** end of the period, represented in UNIX timestamp
- **timezone:** the timezone in which the date/time should be returned
- **limit:** the number of the top N pages that the response should return. It's a positive number. If `0` is passed as a parameter by default it will return only the top 10 pages.

The max available period for fetching analytics data is 30 days. Thus the `from` "oldest" value will always be `now minus 30d`

## Response

The pages endpoint response returns an object with two main properties `data` and `ingestion`.

The `data` property is a collection of objects. Each object has two properties `count` and `resource`:

- **count:** number of the page views
- **resource:** the page path

The `ingestion` property contains general information like `status`, `ingestion_start`, `ingestion_end` where

- **ingestion_start:** the start date for the current analytics tracking. When Netlify started tracking analytics for your site.
- **ingestion_end:** the end date for the current analytics tracking. It's usually the date of the last full day.

```json
{
    "data": [
        {
            "count": 100,
            "resource": "/media/images-gallery"
        },
        {
            "count": 100,
            "resource": "/"
        }
    ],
    "ingestion": {
        "status": "current",
        "ingestion_start": 1605186000000,
        "ingestion_end": 1616151600000
    }
}
```

**Example Request Parameters:**

```text
from=1615978719785
to=1616065119785
timezone=+0200
limit=15
```
