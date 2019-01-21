---
title: Trade Aggregations
---

Trade Aggregations are catered specifically for developers of trading clients. They facilitate efficient gathering of historical trade data. This is done by dividing a given time range into segments and aggregate statistics, for a given asset pair (`base`, `counter`) over each of these segments.


## Request

```
GET /trade_aggregations?base_asset_type={base_asset_type}&base_asset_code={base_asset_code}&base_asset_issuer={base_asset_issuer}&counter_asset_type={counter_asset_type}&counter_asset_code={counter_asset_code}&counter_asset_issuer={counter_asset_issuer}
```

### Arguments

| name | notes | description | example |
| ---- | ----- | ----------- | ------- |
| `start_time` | long | lower time boundary represented as millis since epoch| 1512689100000 |
| `end_time` | long | upper time boundary represented as millis since epoch| 1512775500000|
| `resolution` | long | segment duration as millis since epoch. *Supported values are 1 minute (60000), 5 minutes (300000), 15 minutes (900000), 1 hour (3600000), 1 day (86400000) and 1 week (604800000).*| 300000|
| `base_asset_type` | string | Type of base asset | `native` |
| `base_asset_code` | string | Code of base asset, not required if type is `native` | `USD` |
| `base_asset_issuer` | string | Issuer of base asset, not required if type is `native` | 'GA2HGBJIJKI6O4XEM7CZWY5PS6GKSXL6D34ERAJYQSPYA6X6AI7HYW36' |
| `counter_asset_type` | string | Type of counter asset  | `credit_alphanum4` |
| `counter_asset_code` | string | Code of counter asset, not required if type is `native` | `BTC` |
| `counter_asset_issuer` | string | Issuer of counter asset, not required if type is `native` | 'GATEMHCCKCY67ZUCKTROYN24ZYT5GK4EQZ65JJLDHKHRUZI3EUEKMTCH' |
| `?order`  | optional, string, default `asc` | The order, in terms of timeline, in which to return rows, "asc" or "desc". | `asc` |
| `?limit`  | optional, number, default: `10` | Maximum number of records to return. | `200` |

### curl Example Request
```sh 
curl https://horizon.stellar.org/trade_aggregations?base_asset_type=native&counter_asset_code=SLT&counter_asset_issuer=GCKA6K5PCQ6PNF5RQBF7PQDJWRHO6UOGFMRLK3DYHDOI244V47XKQ4GP&counter_asset_type=credit_alphanum4&limit=200&order=asc&resolution=3600000&start_time=1517521726000&end_time=1517532526000
```

## Response

A list of collected trade aggregations.

Note
- Segments that fit into the time range but have 0 trades in them, will not be included.
- Partial segments, in the beginning and end of the time range, will not be included.

### Example Response
```json
{
  "_links": {
    "self": {
      "href": "https://horizon.stellar.org/trade_aggregations?base_asset_type=native\u0026counter_asset_code=SLT\u0026counter_asset_issuer=GCKA6K5PCQ6PNF5RQBF7PQDJWRHO6UOGFMRLK3DYHDOI244V47XKQ4GP\u0026counter_asset_type=credit_alphanum4\u0026limit=200\u0026order=asc\u0026resolution=3600000\u0026start_time=1517521726000\u0026end_time=1517532526000"
    },
    "next": {
      "href": "https://horizon.stellar.org/trade_aggregations?base_asset_type=native\u0026counter_asset_code=SLT\u0026counter_asset_issuer=GCKA6K5PCQ6PNF5RQBF7PQDJWRHO6UOGFMRLK3DYHDOI244V47XKQ4GP\u0026counter_asset_type=credit_alphanum4\u0026end_time=1517532526000\u0026limit=200\u0026order=asc\u0026resolution=3600000\u0026start_time=1517529600000"
    },
  },
  "_embedded": {
    "records": [
      {
        "timestamp": 1517522400000,
        "trade_count": 26,
        "base_volume": "27575.0201596",
        "counter_volume": "5085.6410385",
        "avg": "0.1844293",
        "high": "0.1915709",
        "high_r": {
          "N": 50,
          "D": 261
        },
        "low": "0.1506024",
        "low_r": {
          "N": 25,
          "D": 166
        },
        "open": "0.1724138",
        "open_r": {
          "N": 5,
          "D": 29
        },
        "close": "0.1506024",
        "close_r": {
          "N": 25,
          "D": 166
        }
      },
      {
        "timestamp": 1517526000000,
        "trade_count": 15,
        "base_volume": "3913.8224543",
        "counter_volume": "719.4993608",
        "avg": "0.1838355",
        "high": "0.1960784",
        "high_r": {
          "N": 10,
          "D": 51
        },
        "low": "0.1506024",
        "low_r": {
          "N": 25,
          "D": 166
        },
        "open": "0.1869159",
        "open_r": {
          "N": 20,
          "D": 107
        },
        "close": "0.1515152",
        "close_r": {
          "N": 5,
          "D": 33
        }
      }
    ]
  }
}
```

## Possible Errors

- The [standard errors](../errors.md#Standard_Errors).