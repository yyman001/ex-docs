# Spot
---
## Public

### Security​

Endpoints under Public section can be accessed freely without requiring any API-key or signatures.

| name              | Request type | Request url                             | remasks                                       |
| ----------------- | ------------ | --------------------------------------- | --------------------------------------------- |
| Check Server Time | get          | https://openapi.xxx.com/sapi/v1/time    |                                               |
| Pairs List        | get          | https://openapi.xxx.com/sapi/v1/symbols |                                               |
| Test Connectivity | get          | https://openapi.xxx.com/sapi/v1/ping    | This endpoint checks connectivity to the host |

### Pairs List  ###

**Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/PairsList.java

**Responses**
| name              | type    | example | description                     |
| ----------------- | ------- | ------- | ------------------------------- |
| baseAsset         | string  | BTC     | Underlying asset for the symbol |
| pricePrecision    | integer | 2       | Precision of the price          |
| quantityPrecision | integer | 6       | Precision of the quantity       |
| quoteAsset        | string  | USDT    | Quote asset for the symbol      |
| symbol            | string  | BTCUSDT | Name of the symbol              |
```json
{
    "symbols": [
        {
            "quantityPrecision": 3,
            "symbol": "sccadai",
            "pricePrecision": 6,
            "baseAsset": "SCCA",
            "quoteAsset": "DAI"
        },
        {
            "quantityPrecision": 8,
            "symbol": "btcusdt",
            "pricePrecision": 2,
            "baseAsset": "BTC",
            "quoteAsset": "USDT"
        },
        {
            "quantityPrecision": 3,
            "symbol": "bchusdt",
            "pricePrecision": 2,
            "baseAsset": "BCH",
            "quoteAsset": "USDT"
        },
        {
            "quantityPrecision": 2,
            "symbol": "etcusdt",
            "pricePrecision": 2,
            "baseAsset": "ETC",
            "quoteAsset": "USDT"
        },
        {
            "quantityPrecision": 2,
            "symbol": "ltcbtc",
            "pricePrecision": 6,
            "baseAsset": "LTC",
            "quoteAsset": "BTC"
        }
    ]
}
```


###  Test Connectivity
**Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/TestConnectivity.java

**Responses**
```json
{}
```

### Check Server Time
**Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CheckServerTime.java

**Responses**

| name       | type   | example       | description      |
| ---------- | ------ | ------------- | ---------------- |
| serverTime | long   | 1607702400000 | 服务器 timestamp |
| timezone   | string | GMT+08:00     | 服务器时区       |


```json
{
    "timezone": "GMT+08:00",
    "serverTime": 1595563624731
}
```

## Market

### Security​

行情下方的接口不需要API-Key或者Sign就能自由访问

| name                   | Request type | Request url                            | remasks                          |
| ---------------------- | ------------ | -------------------------------------- | -------------------------------- |
| 24hrs ticker           | get          | https://openapi.xxx.com/sapi/v1/ticker | 24 hour price change statistics. |
| Depth                  | get          | https://openapi.xxx.com/sapi/v1/depth  | market detpth data               |
| Kline/candlestick data | get          | https://openapi.xxx.com/sapi/v1/klines |                                  |
| Recent Trades List     | get          | https://openapi.xxx.com/sapi/v1/trades |                                  |

### Kline/candlestick data

 **Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/KlineCandlestickData.java

#### Parameters
***Query***
| Parameters name | data type | name                                                                                          |
| --------------- | --------- | --------------------------------------------------------------------------------------------- |
| interval        | string    | Interval of the Kline. Possible values include: 1min,5min,15min,30min,60min,1day,1week,1month |
| limit           | integer   | Default 100; Max 300                                                                          |
| symbol          | string    | Symbol Name E.g. BTCUSDT                                                                      |


**Responses**
| name | type   | example         | description  |
| ---- | ------ | --------------- | ------------ |
| high | float  | `9900`          | High Price   |
| last | float  | `8900`          | Last Price   |
| low  | float  | `8800.34`       | Low Price    |
| rose | string | `+0.5`          | 涨跌幅       |
| time | long   | `1595563624731` | timestamp    |
| vol  | float  | `4999`          | Trade Volume |

```json
[
    {
        "high": "6228.77",
        "vol": "111",
        "low": "6228.77",
        "idx": 1594640340,
        "close": "6228.77",
        "open": "6228.77"
    },
    {
        "high": "6228.77",
        "vol": "222",
        "low": "6228.77",
        "idx": 1587632160,
        "close": "6228.77",
        "open": "6228.77"
    },
    {
        "high": "6228.77",
        "vol": "333",
        "low": "6228.77",
        "idx": 1587632100,
        "close": "6228.77",
        "open": "6228.77"
    }
]
```

### Recent Trades List

 **Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/RecentTradesList.java

#### Parameters
***Query***
| Parameters name | data type | name                            |
| --------------- | --------- | ------------------------------- |
| limit           | string    | Default 100; Max 1000           |
| symbol          | string    | Name of the symbol E.g. BTCUSDT |


**Responses**
| name  | type   | example       | description            |
| ----- | ------ | ------------- | ---------------------- |
| price | float  | 0.055         | The price of the trade |
| qty   | float  | 5             | The quantity traded    |
| side  | string | BUY/SELL      | Taker side             |
| time  | long   | 1537797044116 | Current timestamp (ms) |

```json
{
    "list":[
        {
            "price":"3.00000100",
            "qty":"11.00000000",
            "time":1499865549590,
            "side":"BUY"
        }
    ]
}
```


###  24hrs ticker

!原文档有参数有错误~ `close` -> `open`
**Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Ticker.java

#### Parameters
***Query***
| Parameters name | data type | name                     |
| --------------- | --------- | ------------------------ |
| symbol          | string    | Symbol Name E.g. BTCUSDT |

**Responses**
| name | type  | example       | description   |
| ---- | ----- | ------------- | ------------- |
| high | float | 9900          | high price    |
| last | float | 8900          | Last Price    |
| low  | float | 8800.34       | Low Price     |
| open | float | 5000          | opening price |
| time | long  | 1595563624731 | Open Time     |
| vol  | float | 4999          | Trade Volume  |


```json
{
    "high": "9279.0301",
    "vol": "1302",
    "last": "9200",
    "low": "9279.0301",
    "rose": "0",
    "time": 1595563624731
}
```


### Depth
**Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Depth.java

#### Parameters
***Query***
| Parameters name | data type | name                     |
| --------------- | --------- | ------------------------ |
| limit           | integer   | Default 100; Max 100     |
| symbol          | string    | Symbol Name E.g. BTCUSDT |

**Responses**
| name | type | example       | description                                                     |
| ---- | ---- | ------------- | --------------------------------------------------------------- |
| asks | list |               | List of all asks, best asks first. See below for entry details. |
| bids | list |               | List of all bids, best bids first. See below for entry details. |
| time | long | 1595563624731 | Current timestamp (ms)                                          |

The fields bids and asks are lists of order book price level entries, sorted from best to worst.

| name | type  | example | description                                       |
| ---- | ----- | ------- | ------------------------------------------------- |
| ' '  | float | 131.1   | price level                                       |
| ' '  | float | 2.3     | The total quantity of orders for this price level |

```json
{
  "bids": [
    [
      "3.90000000",   // price
      "431.00000000"  // vol
    ],
    [
      "4.00000000",
      "431.00000000"
    ]
  ],
  "asks": [
    [
      "4.00000200",  // price
      "12.00000000"  // vol
    ],
    [
      "5.10000000",
      "28.00000000"
    ]
  ]
}
```



### Trade

安全type: [TRADE]
Endpoints under Trade require an

| name                | Request type | Request url                                 | remasks                                                                                                                                          |
| ------------------- | ------------ | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Batch Cancel Orders | post         | https://openapi.xxx.com/sapi/v1/batchCancel | Rate Limit: 50times/2s A batch contains at most 10 orders                                                                                        |
| Batch Orders        | post         | https://openapi.xxx.com/sapi/v1/batchOrders | Rate Limit: 50times/2s A batch contains at most 10 orders                                                                                        |
| Cancel Orders       | post         | https://openapi.xxx.com/sapi/v1/cancel      | RATE LIMIT: 100times/2s                                                                                                                          |
| Current Open Orders | get          | https://openapi.xxx.com/sapi/v1/openOrders  | Rate Limit: 20times/2s                                                                                                                           |
| New Order           | post         | https://openapi.xxx.com/sapi/v1/order       | RATE LIMIT: 100TIMES/2s                                                                                                                          |
| Query Order         | get          | https://openapi.xxx.com/sapi/v1/order       | Rate Limit: 20times/2s                                                                                                                           |
| Test New Order      | post         | https://openapi.xxx.com/sapi/v1/order/test  | Test new order creation and signature/recvWindow length. Creates and validates a new order but does not send the order into the matching engine. |
| Trades              | get          | https://openapi.xxx.com/sapi/v1/myTrades    | Rate Limit: 20times/2s                                                                                                                           |

### Trades

 **Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Trades.java 

#### Parameters
***Query***
| Parameters name | data type | name                            |
| --------------- | --------- | ------------------------------- |
| fromId          | integer   | Trade Id to fetch from          |
| limit           | string    | Default 100; Max 1000           |
| symbol          | string    | Name of the symbol E.g. BTCUSDT |

***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | Sign         |
| X-CH-TS         | integer   | timestamp    |

**Responses**
| name    | type    | example            | description               |
| ------- | ------- | ------------------ | ------------------------- |
| askId   | long    | 150695552109032493 | Ask Order ID              |
| bidId   | long    | 150695552109032492 | Bid Order ID              |
| fee     | number  | 0.001              | Trading fee               |
| feeCoin | string  | ETH                | Trading fee coin          |
| id      | integer | 28457              | Trade ID                  |
| isBuyer | bool    | true               | true= Buyer false= Seller |
| isMaker | bool    | false              | true=Maker false=Taker    |
| price   | integer | 4.01               | Price of the trade        |
| qty     | float   | 12                 | Quantiry of the trade     |
| symbol  | string  | ETHBTC             | Symbol Name               |
| time    | number  | 1499865549590      | timestamp of the trade    |


```json
[
  {
    "symbol": "ETHBTC",
    "id": 100211,
    "bidId": 150695552109032492,
    "askId": 150695552109032493,
    "price": "4.00000100",
    "qty": "12.00000000",
    "time": 1499865549590,
    "isBuyer": true,
    "isMaker": false,
    "feeCoin": "ETH",
    "fee":"0.001"
  },...
]
```


###  New Order

 **Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/NewOrder.java

#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | Sign         |
| X-CH-TS         | integer   | timestamp    |

***Body***
| Parameters name  | data type | name                                                    |
| ---------------- | --------- | ------------------------------------------------------- |
| newClientOrderId | string    | Unique order ID generated by users to mark their orders |
| price            | number    | Order price, REQUIRED for LIMIT orders                  |
| recvWindow       | integer   | Time window                                             |
| side             | string    | Side of the order,BUY/SELL                              |
| symbol           | string    | Name of the symbol E.g. BTCUSDT                         |
| type             | string    | Type of the order, LIMIT/MARKET                         |
| volume           | number    | Order vol. For MARKET BUY orders, vol=amount.           |


**Responses**
| name          | type    | example            | description                                                                                           |
| ------------- | ------- | ------------------ | ----------------------------------------------------------------------------------------------------- |
| clientOrderId | string  | 213443             | A unique ID of the order.                                                                             |
| executedQty   | float   | 1.01               | Quantity of orders that has been executed                                                             |
| orderId       | long    | 150695552109032492 | ID of the order                                                                                       |
| origQty       | float   | 1.01               | Quantity ordered                                                                                      |
| price         | float   | 4765.29            | Price of the order                                                                                    |
| side          | string  | BUY                | Order side：BUY, SELL                                                                                 |
| status        | string  | NEW                | The state of the order.Possible values include NEW, PARTIALLY_FILLED, FILLED, CANCELED, and REJECTED. |
| symbol        | string  | BTCUSDT            | Symbol Name                                                                                           |
| transactTime  | integer | 1273774892913      | Time the order is placed                                                                              |
| type          | string  | LIMIT              | Order type LIMIT,MARKET                                                                               |

```json
{
    'symbol': 'LXTUSDT', 
    'orderId': '150695552109032492', 
    'clientOrderId': '157371322565051',
    'transactTime': '1573713225668', 
    'price': '0.005452', 
    'origQty': '110', 
    'executedQty': '0', 
    'status': 'NEW',
    'type': 'LIMIT', 
    'side': 'SELL'
}
```
###  Test New Order
 **Demo:** 
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/TestNewOrder.java

#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | Sign         |
| X-CH-TS         | integer   | timestamp    |

***Body***
| Parameters name  | data type | name                                                    |
| ---------------- | --------- | ------------------------------------------------------- |
| newClientOrderId | string    | Unique order ID generated by users to mark their orders |
| price            | number    | Order price, REQUIRED for LIMIT orders                  |
| recvWindow       | integer   | Time window                                             |
| side             | string    | Side of the order,BUY/SELL                              |
| symbol           | string    | Name of the symbol E.g. BTCUSDT                         |
| type             | string    | Type of the order, LIMIT/MARKET                         |
| volume           | number    | Order vol. For MARKET BUY orders, vol=amount            |

**Responses**
```json
{}
```


###  Current Open Orders

**Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CurrentOpenOrders.java 

#### Parameters
***Query***
| Parameters name | data type | name                            |
| --------------- | --------- | ------------------------------- |
| limit           | integer   | Default 100; Max 1000           |
| symbol          | string    | Name of the symbol E.g. BTCUSDT |

***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | Sign         |
| X-CH-TS         | integer   | timestamp    |

**Responses**
| name          | type   | example            | description                                                                                           |
| ------------- | ------ | ------------------ | ----------------------------------------------------------------------------------------------------- |
| avgPrice      | float  | 4754.24            | Average price of filled orders.                                                                       |
| clientOrderId | string | 213443             | Unique ID of the order.                                                                               |
| executedQty   | float  | 1.01               | Quantity of orders that has been executed                                                             |
| orderId       | long   | 150695552109032492 | ID of the order                                                                                       |
| origQty       | float  | 1.01               | Quantity ordered                                                                                      |
| price         | float  | 4765.29            | Price of the order                                                                                    |
| side          | string | BUY                | The order side BUY,SELL                                                                               |
| status        | string | NEW                | The state of the order.Possible values include NEW, PARTIALLY_FILLED, FILLED, CANCELED, and REJECTED. |
| symbol        | string | BTCUSDT            | Name of the symbol                                                                                    |
| type          | string | LIMIT              | The order typeLIMIT,MARKET                                                                            |


```json
[
    {
        'orderId': '499902955766523648', 
        'symbol': 'BHTUSDT', 
        'price': '0.01', 
        'origQty': '50', 
        'executedQty': '0', 
        'avgPrice': '0', 
        'status': 'NEW', 
        'type': 'LIMIT', 
        'side': 'BUY', 
        'time': '1574329076202'
        },...
]
```

### Batch Orders

 **Demo:** 
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/BatchOrders.java

#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | Sign         |
| X-CH-TS         | integer   | timestamp    |

***Body***
| Parameters name | data type | name                            |
| --------------- | --------- | ------------------------------- |
| orders          | array     | Batch order param               |
| symbol          | string    | Name of the symbol E.g. BTCUSDT |

**Responses**
`orders` field:
| name      | type   | example      | description             |
| --------- | ------ | ------------ | ----------------------- |
| batchType | string | LIMIT/MARKET | Batch type of the order |
| price     | folat  | 1000         | Price of the order      |
| side      | string | BUY/SELL     | Side of the order       |
| volume    | folat  | 20.1         | Vol of the order        |

```json
{
    "ids": [
        165964665990709251,
        165964665990709252,
        165964665990709253
    ]
}
```

### Current Open Orders

**Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/BatchCancelOrders.java

#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | Sign         |
| X-CH-TS         | integer   | timestamp    |

***Body***
| Parameters name | data type | name                            |
| --------------- | --------- | ------------------------------- |
| orderIds        | array     | Order ID collection [123,456]   |
| symbol          | string    | Name of the symbol E.g. BTCUSDT |

**Responses**
| name | type | example | description |
| ---- | ---- | ------- | ----------- |


```json
{
    "success": [
        165964665990709251,
        165964665990709252,
        165964665990709253
    ],
    "failed": [ //取消失败一般是因为订单不存在或订单状态已经到终态
        165964665990709250  
    ]
}
```

### Cancel Orders

 **Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CancelOrder.java 

#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | Sign         |
| X-CH-TS         | integer   | timestamp    |

***Body***
| Parameters name  | data type | name                                                    |
| ---------------- | --------- | ------------------------------------------------------- |
| newClientOrderId | string    | Unique order ID generated by users to mark their orders |
| orderId          | string    | 订单 id                                                 |
| symbol           | string    | Name of the symbol E.g. BTCUSDT                         |


**Responses**
| name          | type   | example            | description                                                                                           |
| ------------- | ------ | ------------------ | ----------------------------------------------------------------------------------------------------- |
| clientOrderId | string | 213443             | Unique ID of the order.                                                                               |
| orderId       | long   | 150695552109032492 | ID of the order                                                                                       |
| status        | string | NEW                | The state of the order.Possible values include NEW, PARTIALLY_FILLED, FILLED, CANCELED, and REJECTED. |
| symbol        | string | BHTUSDT            | Name of the symbol                                                                                    |

```json
{
    'symbol': 'BHTUSDT', 
    'clientOrderId': '0', 
    'orderId': '499890200602846976', 
    'status': 'CANCELED'
}

```



### Query Order

 **Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/QueryOrder.java 

#### Parameters
***Query***
| Parameters name  | data type | name                                                    |
| ---------------- | --------- | ------------------------------------------------------- |
| newClientOrderId | string    | Unique order ID generated by users to mark their orders |
| orderId          | string    | 订单 id                                                 |
| symbol           | string    | Name of the symbol E.g. BTCUSDT                         |

***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | Sign         |
| X-CH-TS         | integer   | timestamp    |


**Responses**
| name          | type   | example            | description                                                                                           |
| ------------- | ------ | ------------------ | ----------------------------------------------------------------------------------------------------- |
| avgPrice      | float  | 4754.24            | Average price of filled orders.                                                                       |
| clientOrderId | string | 213443             | Unique ID of the order.                                                                               |
| executedQty   | float  | 1.01               | Quantity of orders that has been executed                                                             |
| orderId       | long   | 150695552109032492 | ID of the order                                                                                       |
| origQty       | float  | 1.01               | Quantity ordered                                                                                      |
| price         | float  | 4765.29            | Price of the order                                                                                    |
| side          | string | BUY                | The order side BUY,SELL                                                                               |
| status        | string | NEW                | The state of the order.Possible values include NEW, PARTIALLY_FILLED, FILLED, CANCELED, and REJECTED. |
| symbol        | string | BTCUSDT            | Name of the symbol                                                                                    |
| type          | string | LIMIT              | The order typeLIMIT,MARKET                                                                            |


```json
{
    'orderId': '499890200602846976', 
    'clientOrderId': '157432755564968', 
    'symbol': 'BHTUSDT', 
    'price': '0.01', 
    'origQty': '50', 
    'executedQty': '0', 
    'avgPrice': '0', 
    'status': 'NEW', 
    'type': 'LIMIT', 
    'side': 'BUY', 
    'transactTime': '1574327555669'
}
```


## Account

Security Type: [USER\_DATA]

| name    | Request type | Request url                             | remasks                |
| ------- | ------------ | --------------------------------------- | ---------------------- |
| Account | get          | https://openapi.xxx.com/sapi/v1/account | Rate Limit: 20times/2s |

### Account Information

**Demo:**
https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/AccountInformation.java

#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | Sign         |
| X-CH-TS         | integer   | timestamp    |

**Responses**
| name     | type  | example              | description |
| -------- | ----- | -------------------- | ----------- |
| balances | Array | Show balance details |


| name   | type   | example | description                     |
| ------ | ------ | ------- | ------------------------------- |
| asset  | string | USDT    | Name of the asset               |
| free   | float  | 1000.30 | Amount available for use        |
| locked | float  | 400     | Amount locked (for open orders) |

```json
{
    'balances': 
        [
            {
                'asset': 'BTC', 
                'free': '0', 
                'locked': '0'
                }, 
            {
                'asset': 'ETH', 
                'free': '0', 
                'locked': '0'
                }
        ]
}
```







