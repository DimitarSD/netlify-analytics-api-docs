# Page Views

> To test the GET request an OAuth 2.0 token is required
>
> **GET Request URL:** `https://analytics.services.netlify.com/v1/[API_ID]/pageviews`

## Request

The page views endpoint request takes four parameters: `from`, `to`, `timezone`, and `resolution`.

- **from:** start of the period, represented in UNIX timestamp in milliseconds
- **to:** end of the period, represented in UNIX timestamp in milliseconds
- **timezone:** the timezone in which the date/time should be returned; the property is optional and it can be skipped
- **resolution:** it takes either of two values `day` or `range`

The max available period for fetching analytics data is 30 days. Thus the `from` "oldest" value will always be `now minus 30d`

## Response

The page views response returns an object with two main properties `data` and `ingestion`. The `data` property is a collection of arrays. In each array, the first parameter is the day (if `day` was passed as a value to `resolution`) and the second parameter is the page views for that day.

The `ingestion` property contains general information like `status`, `ingestion_start`, `ingestion_end` where

- **ingestion_start:** the start date for the current analytics tracking. When Netlify started tracking analytics for your site.
- **ingestion_end:** the end date for the current analytics tracking. It's usually the date of the last full day.

```json
{
    "data": [
        [
            1613253600000,
            200
        ],
        [
            1613340000000,
            300
        ]
    ],
    "ingestion": {
        "status": "current",
        "ingestion_start": 1605186000000,
        "ingestion_end": 1615978800000
    }
}
```

In the case `range` was passed instead of `day`, the `data` collection will contain only one element.  The first value should be ignored, and the second one is the total page views

```json
{
    "data": [
        [
            -62169991200000,
            10300
        ]
    ],
    "ingestion": {
        "status": "current",
        "ingestion_start": 1605186000000,
        "ingestion_end": 1615978800000
    }
}
```

**Example Request Parameters:**

```text
from=1613340000000
to=1616018399999
timezone=+0200
resolution=day
```
