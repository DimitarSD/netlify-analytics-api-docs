# Bandwidth

> To test the GET request an OAuth 2.0 token is required
>
> **GET Request URL:** `https://analytics.services.netlify.com/v1/[API_ID]/bandwidth`

## Request

The bandwidth endpoint request takes five parameter: `from`, `to`, `timezone`, `account_id` and `resolution`.

- **from:** start of the period, represented in UNIX timestamp in milliseconds
- **to:** end of the period, represented in UNIX timestamp in milliseconds
- **timezone:** the timezone in which the date/time should be returned; the property is optional and it can be skipped
- **account_id:** the account id; the property is optional and it can be skipped. However, the response will return `0` for `accountBandwidth`
- **resolution:** it takes either of two values `hour` or `range`

The max available period for fetching analytics data is 30 days. Thus the `from` "oldest" value will always be `now minus 30d x 24h`

## Response

The bandwidth endpoint response returns an object with two main properties `data` and `ingestion`. The `data` property is a collection of objects.

Each object have four properties: `start`, `end`, `siteBandwidth`, `accountBandwidth` where

- **start:** start of the hour period; a UNIX timestamp in milliseconds
- **end:** end of the hour period; a UNIX timestamp in milliseconds
- **siteBandwidth:** the site bandwidth, returned in bytes
- **accountBandwidth:** the account bandwidth, returned in bytes

The `ingestion` property contains general information like `status`, `ingestion_start`, `ingestion_end` where

- **ingestion_start:** the start date for the current analytics tracking. When Netlify started tracking analytics for your site.
- **ingestion_end:** the end date for the current analytics tracking. It's usually the date of the last full day.

```json
{
    "data": [
        {
            "start": 1615975200000,
            "end": 1615978800000,
            "siteBandwidth": 560000000,
            "accountBandwidth": 560000000
        },
        {
            "start": 1615978800000,
            "end": 1615982400000,
            "siteBandwidth": 560000000,
            "accountBandwidth": 560000000
        }
    ],
    "ingestion": {
        "status": "current",
        "ingestion_start": 1605186000000,
        "ingestion_end": 1616065200000
    }
}
```

In the case `range` was passed instead of `hour`, the `data` collection will contain only one element (an object). The `start` and `end` value should be ignored, and `siteBandwidth` and `accountBandwidth` return respectively the total page bandwidth (in bytes) for that rage (specified in `from` and `to`)

```json
{
    "data": [
        {
            "start": -62169991200000,
            "end": 1616104799000,
            "siteBandwidth": 16500000000,
            "accountBandwidth": 16500000000
        }
    ],
    "ingestion": {
        "status": "current",
        "ingestion_start": 1605186000000,
        "ingestion_end": 1616151600000
    }
}
````

**Example Request Parameters:**

```text
from=1615978719777
to=1616065119777
timezone=+0200
account_id=[ACCOUNT_ID]
resolution=hour
```
