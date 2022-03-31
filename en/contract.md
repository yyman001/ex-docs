# Contract
## Public

### Security​: [None]​

Endpoints under Public section can be accessed freely without requiring any API-key or signatures.

| name              | Request type | Request url                                      | remasks                |
| ----------------- | ------------ | ------------------------------------------------ | ---------------------- |
| Check Server Time | get          | https://futuresopenapi.xxx.com/fapi/v1/time      |                        |
| Contract List     | get          | https://futuresopenapi.xxx.com/fapi/v1/contracts |                        |
| 测试连接          | get          | https://futuresopenapi.xxx.com/fapi/v1/ping      | 测试 REST API 的连通性 |

### Contract List ###
`接口参数有误`!
**Responses**
| name            | TYPE   | EXAMPLE    | DESCRIPTION                                                                       |
| --------------- | ------ | ---------- | --------------------------------------------------------------------------------- |
| maxLimitVolume  | number | 100000     | Limit price order maximum volume                                                  |
| maxMarketMoney  | number | 100000     | Market price order maximum value                                                  |
| maxMarketVolume | number | 100000     | Market price order maximum volume                                                 |
| maxValidOrder   | number | 100000     | Maximum valid order quantity                                                      |
| minOrderMoney   | number | 10         | Minimum order value                                                               |
| minOrderVolume  | number | 10         | Minimum order volume                                                              |
| multiplier      | number | 0.5        | Contract face value                                                               |
| multiplierCoin  | string | BTC        | Contract face value unit                                                          |
| pricePrecision  | number | 4          | Precision of the price                                                            |
| side            | number | 1          | Contract direction(backwards：0，1：forward)                                      |
| status          | number | 1          | status（0：cannot trade，1：can trade                                             |
| symbol          | string | E-BTC-USDT | Contract name                                                                     |
| type            | string | S          | contract type, E: perpetual contract, S: test contract, others are mixed contract |

`maxLimitMoney` 参数有误!
```json
[
    {
        "maxLimitVolume": 1000000,
        "maxLimitMoney": 1000000,
        "maxMarketVolume": 100000,
        "maxMarketMoney": 10000000,
        "maxValidOrder": 20,
        "minOrderMoney": 0.001,
        "minOrderVolume": 1,
        "pricePrecision": 8,
        "multiplier": 6,
        "multiplierCoin": "HT",
        "symbol": "H-HT-USDT",
        "side": 1,
        "type": "H",
        "status": 1
    }
]
```

#### 测试连接
**Responses**
```json
{}
```

#### Check Server Time
**Responses**
| name       | type   | example             | description      |
| ---------- | ------ | ------------------- | ---------------- |
| serverTime | long   | 1607702400000       | server timestamp |
| timezone   | string | China standard time | server time zone |


```json
{
    "serverTime":1607702400000,
    "timezone": 中国标准时间
}
```


## MARKET

### Security​: [None]​

Endpoints under Public section can be accessed freely without requiring any API-key or signatures.

| name                   | Request type | Request url                                   | remasks             |
| ---------------------- | ------------ | --------------------------------------------- | ------------------- |
| 24hrs ticker           | get          | https://futuersopenapi.xxx.com/fapi/v1/ticker | 24 小时价格变化数据 |
| Depth                  | get          | https://futuresopenapi.xxx.com/fapi/v1/depth  | market detpth data  |
| Get index/marked price | get          | https://futuersopenapi.xxx.com/fapi/v1/index  |                     |
| Kline/candlestick data | get          | https://futuresopenapi.xxx.com/fapi/v1/klines |                     |

### Kline/candlestick data
#### Parameters
***Query***
| Parameters name | data type | name                                                                                          |
| --------------- | --------- | --------------------------------------------------------------------------------------------- |
| contractName    | string    | Name of the symbol e.g. E-BTC-USDT                                                            |
| interval        | string    | Interval of the Kline. Possible values include: 1min,5min,15min,30min,60min,1day,1week,1month |
| limit           | integer   | Default 100; Max 300                                                                          |


**Responses**
| name  | type  | example       | description           |
| ----- | ----- | ------------- | --------------------- |
| close | float | 33.00000      | Closing price         |
| high  | float | 36.00000      | Max price             |
| idx   | long  | 1538728740000 | Start timestamp (ms） |
| low   | float | 30.00000      | Min price             |
| open  | float | 36.00000      | Open price            |
| vol   | float | 2456.111      | Trade volume          |

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

### Get index/marked price
#### Parameters
***Query***
| Parameters name | data type | name                               |
| --------------- | --------- | ---------------------------------- |
| contractName    | string    | Name of the symbol e.g. E-BTC-USDT |
| limit           | string    | Default 100; Max 300               |


**Responses**
| name            | type   | example    | Description       |
| --------------- | ------ | ---------- | ----------------- |
| contractName    | string | E-BTC-USDT | Contract name     |
| indexPrice      | float  | 0.055      | Index price       |
| lastFundingRate | float  | 0.123      | Current fund rate |
| markPrice       | float  | 0.0578     | Marked price      |

```json
{
    "markPrice": 581.5,
    "indexPrice": 646.3933333333333,
    "lastFundingRate": 0.001,
    "contractName": "E-ETH-USDT",
    "time": 1608273554063
}
```

### 24hrs ticker
#### Parameters
***Query***
| Parameters name | data type | name                               |
| --------------- | --------- | ---------------------------------- |
| contractName    | string    | Name of the symbol e.g. E-BTC-USDT |

**Responses**
| name | type   | example       | description     |
| ---- | ------ | ------------- | --------------- |
| high | float  | 9900          | Higher price    |
| last | float  | 8900          | Newest price    |
| low  | float  | 8800.34       | Lower price     |
| rose | string | +0.5          | Price variation |
| time | long   | 1595563624731 | Open time       |
| vol  | float  | 4999          | Trade volume    |

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
#### Parameters
***Query***
| Parameters name | data type | name                               |
| --------------- | --------- | ---------------------------------- |
| contractName    | string    | Name of the symbol e.g. E-BTC-USDT |
| limit           | integer   | Default 100; Max 300               |

**Responses**
| name | type | example       | description              |
| ---- | ---- | ------------- | ------------------------ |
| asks | list | Look below    | Order book selling info  |
| bids | list | Look below    | Order book purchase info |
| time | long | 1595563624731 | Current Timestamp (ms)   |


| name | type  | example | description                               |
| ---- | ----- | ------- | ----------------------------------------- |
| ' '  | float | 131.1   | price level                               |
| ' '  | float | 2.3     | Total order quantity for this price level |

```json
{
  "bids": [
    [
      "3.90000000",   // 价格
      "431.00000000"  // 数量
    ],
    [
      "4.00000000",
      "431.00000000"
    ]
  ],
  "asks": [
    [
      "4.00000200",  // 价格
      "12.00000000"  // 数量
    ],
    [
      "5.10000000",
      "28.00000000"
    ]
  ]
}
```


## 交易相关

Security​: [TRADE]
​
| name                     | Request type | Request url                                              | remasks                                                               |
| ------------------------ | ------------ | -------------------------------------------------------- | --------------------------------------------------------------------- |
| Cancel order             | post         | https://futuresopenapi.xxx.com/fapi/v1/cancel            | Rate Limit: 20times/2s                                                |
| Condition order creation | post         | https://futuresopenapi.xxx.com/fapi/v1/conditionOrder    |                                                                       |
| Open order               | get          | https://futuresopenapi.xxx.com/fapi/v1/openOrders        | Speed limit rules:                                                    |
| Order Historical         | post         | https://futuresopenapi.xxx.com/fapi/v1/orderHistorical   |                                                                       |
| Order creation           | post         | https://futuresopenapi.xxx.com/fapi/v1/order             | Order creation                                                        |
| Order details            | get          | https://futuresopenapi.xxx.com/fapi/v1/order             |                                                                       |
| Order record             | get          | https://futuresopenapi.xxx.com/fapi/v1/myTrades          | Rate Limit: 20times/2s Obtain open contract, the user's current order |
| Profit Historical        | post         | https://futuresopenapi.xxx.com/fapi/v1/Profit Historical |                                                                       |
 
### Order record
#### Parameters
***Query***
| Parameters name | data type | name                               |
| --------------- | --------- | ---------------------------------- |
| contractName    | string    | Name of the symbol e.g. E-BTC-USDT |
| fromId          | long      | Trade Id to fetch from             |
| limit           | string    | Default 100; Max 1000              |

***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | YOUR API-key |
| X-CH-SIGN       | string    | SIGN         |
| X-CH-TS         | integer   | TIMESTAMP    |

**Responses**
| name         | TYPE    | EXAMPLE            | DESCRIPTION                                        |
| ------------ | ------- | ------------------ | -------------------------------------------------- |
| amount       | float   | 5.38               | Filled amount                                      |
| askId        | long    | 150695552109032493 | Seller order ID                                    |
| askUserId    | integer | 10025              | Seller user ID                                     |
| bidId        | long    | 150695552109032492 | Buyer order ID                                     |
| bidUserId    | integer | 10024              | Buyer user ID                                      |
| contractName | string  | E-BTC-USDT         | Contract name                                      |
| fee          | number  | 0.001              | Trading fees                                       |
| isBuyer      | boolean | true               | is it buyer?                                       |
| isMaker      | boolean | true               | is it maker?                                       |
| price        | float   | 4.01               | Filled price                                       |
| qty          | float   | 12                 | Trade quantity                                     |
| side         | string  | buy                | Current order direction BUY purchase, SELL selling |
| symbol       | string  | ETHBTC             | Coin name(trade pair)                              |
| time         | number  | 1499865549590      | Trade time stamp                                   |
| tradeId      | number  | 28457              | Trade ID                                           |

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
    "fee":"0.001"
  },...
]
```

### Condition order creation
#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | SIGN         |
| X-CH-TS         | string    | TIMESTAMP    |

***Body***
| Parameters name | data type | name                                                      |
| --------------- | --------- | --------------------------------------------------------- |
| clientOrderId   | string    | 213443                                                    |
| contractName    | string    | Contract name 如 `E-BTC-USDT`                             |
| open            | string    | Open balancing direction, `OPEN/CLOSE`                    |
| positionType    | number    | Hold-up position, 1 full position, 2 restrictive position |
| price           | number    | Order price, REQUIRED for LIMIT orders                    |
| side            | string    | Side of the order,BUY/SELL                                |
| triggerPrice    | string    | Trigger Price                                             |
| triggerType     | string    | Trigger Type `3UP/4DOWN`                                  |
| type            | string    | Type of the order, LIMIT/MARKET                           |
| volume          | number    | Order vol. For MARKET BUY orders, vol=amount.             |


**Responses**
| name    | TYPE   | EXAMPLE              | DESCRIPTION |
| ------- | ------ | -------------------- | ----------- |
| orderId | string | `256609229205684228` | Order ID    |

```json
{
    "orderId": 256609229205684228
}
```

### Order creation

#### Parameters

***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | SIGN         |
| X-CH-TS         | string    | TIMESTAMP    |

***Body***
| Parameters name | data type | name                                                         |
| --------------- | --------- | ------------------------------------------------------------ |
| clientOrderId   | string    | Client order identity, a string with length less than 32 bit |
| contractName    | string    | Contract name 如 `E-BTC-USDT`                                |
| open            | string    | Open balancing direction,, `OPEN/CLOSE`                      |
| positionType    | number    | Hold-up position, 1 full position, 2 restrictive position                            |
| price           | number    | Order price                                                  |
| side            | string    | trade direction, `BUY/SELL`                                  |
| timeInForce     | string    | `IOC, FOK, POST_ONLY`                                        |
| type            | string    | Order type, LIMIT/MARKET                                     |
| volume          | number    | Order quantity                                               |

**Responses**
| name    | TYPE   | EXAMPLE              | DESCRIPTION |
| ------- | ------ | -------------------- | ----------- |
| orderId | string | `256609229205684228` | Order ID    |

```json
{
    "orderId": 256609229205684228
}
```


### Order Historical
#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | SIGN         |
| X-CH-TS         | string    | TIMESTAMP    |

***Body***
| Parameters name | data type | name                               |
| --------------- | --------- | ---------------------------------- |
| contractName    | string    | Name of the symbol e.g. E-BTC-USDT |
| fromId          | long      | Trade Id to fetch from             |
| limit           | string    | Default 100; Max 1000              |

**Responses**
| name | TYPE | EXAMPLE | DESCRIPTION |
| ---- | ---- | ------- | ----------- |



```json
[
    {
        "side":"BUY",
        "clientId":"0",
        "ctimeMs":1632903411000,
        "positionType":2,
        "orderId":777293886968070157,
        "avgPrice":41000,
        "openOrClose":"OPEN",
        "leverageLevel":26,
        "type":4,
        "closeTakerFeeRate":0.00065,
        "volume":2,
        "openMakerFeeRate":0.00025,
        "dealVolume":1,
        "price":41000,
        "closeMakerFeeRate":0.00025,
        "contractId":1,
        "ctime":"2021-09-29T16:16:51",
        "contractName":"E-BTC-USDT",
        "openTakerFeeRate":0.00065,
        "dealMoney":4.1,
        "status":4
    }
]
```

### Cancel order
#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | SIGN         |
| X-CH-TS         | integer   | TIMESTAMP    |

***Body***
| Parameters name | data type | name                     |
| --------------- | --------- | ------------------------ |
| contractName    | string    | Contract name E-BTC-USDT |
| orderId         | string    | ID of the order          |

**Responses**
| name    | TYPE   | EXAMPLE              | DESCRIPTION     |
| ------- | ------ | -------------------- | --------------- |
| orderId | string | `256609229205684228` | ID of the order |

```json
{
    "orderId": 256609229205684228
}
```


### Open order
#### Parameters
***Query***
| Parameters name | data type | name                     |
| --------------- | --------- | ------------------------ |
| contractName    | string    | Contract name E-BTC-USDT |

***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | YOUR API-key |
| X-CH-SIGN       | string    | SIGN         |
| X-CH-TS         | string    | TIMESTAMP    |

**Responses**
| name         | type   | example            | description                                                                                                                                                                              |
| ------------ | ------ | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| action       | string | OPEN               | OPEN/CLOSE                                                                                                                                                                               |
| avgPrice     | float  | 4754.24            | Filled orders average price                                                                                                                                                              |
| contractName | string | E-BTC-USDT         | Contract name                                                                                                                                                                            |
| executedQty  | float  | 1.01               | Filled orders quantity                                                                                                                                                                   |
| orderId      | long   | 150695552109032492 | Order ID（system generated）                                                                                                                                                             |
| origQty      | float  | 1.01               | Order quantity                                                                                                                                                                           |
| price        | float  | 4765.29            | Order price                                                                                                                                                                              |
| side         | string | BUY                | Order direction. Possible values can only be：BUY（buy long）and SELL（sell short）                                                                                                      |
| status       | string | NEW                | Order status. Possible values are：NEW(new order，not filled)、PARTIALLY_FILLED（partially filled）、FILLED（fully filled）、CANCELLED（already cancelled）andREJECTED（order rejected） |
| transactTime | long   | 1607702400000      | Order creation time,                                                                                                                                                                     |
| type         | string | LIMIT              | Order type. Possible values can only be:LIMIT(limit price) andMARKET（market price）                                                                                                     |

```json
[
    {
       "side": "BUY",
       "executedQty": 0,
       "orderId": 259396989397942275,
       "price": 10000.0000000000000000,
       "origQty": 1.0000000000000000,
       "avgPrice": 0E-8,
       "transactTime": "1607702400000",
       "action": "OPEN",
       "contractName": "E-BTC-USDT",
       "type": "LIMIT",
       "status": "INIT"
    }
]

```


### Profit Historical
#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | Your API-key |
| X-CH-SIGN       | string    | SIGN         |
| X-CH-TS         | string    | TIMESTAMP    |

***Body***
| Parameters name | data type | name                       |
| --------------- | --------- | -------------------------- |
| contractName    | string    | Contract name `E-BTC-USDT` |
| fromId          | long      | Trade Id to fetch from     |
| limit           | string    | Default 100; Max 1000      |

**Responses**
| name | TYPE | EXAMPLE | DESCRIPTION |
| ---- | ---- | ------- | ----------- |




```json
[
    {
        "side":"SELL",
        "positionType":2,
        "tradeFee":-5.23575,
        "realizedAmount":0,
        "leverageLevel":26,
        "openPrice":44500,
        "settleProfit":0,
        "mtime":1632882739000,
        "shareAmount":0,
        "openEndPrice":44500,
        "closeProfit":-45,
        "volume":900,
        "contractId":1,
        "historyRealizedAmount":-50.23575,
        "ctime":1632882691000,
        "id":8764,
        "capitalFee":0
    }
]
```


### Order details
#### Parameters
***Query***
| Parameters name | data type | name                      |
| --------------- | --------- | ------------------------- |
| clientOrderId   | string    | A unique ID of the order. |
| contractName\*  | string    | Contract name             |
| orderId\*       | string    | ID of the order           |

**Responses**
| name         | type   | example            | description                                                                                                                                                                              |
| ------------ | ------ | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| action       | string | OPEN               | OPEN/CLOSE                                                                                                                                                                               |
| avgPrice     | float  | 10.5               | Average transaction price                                                                                                                                                                |
| contractName | string | E-BTC-USDT         | Contract name                                                                                                                                                                            |
| executedQty  | float  | 20                 | Order quantity                                                                                                                                                                           |
| orderId      | long   | 150695552109032492 | Order ID（system generated                                                                                                                                                               |
| origQty      | float  | 10.5               | Order quantity                                                                                                                                                                           |
| price        | float  | 10.5               | Order price                                                                                                                                                                              |
| side         | string | NEW                | Order direction. Possible values can only be：BUY（buy long）and SELL（sell short）                                                                                                      |
| status       | string | NEW                | Order status. Possible values are：NEW(new order，not filled)、PARTIALLY_FILLED（partially filled）、FILLED（fully filled）、CANCELLED（already cancelled）andREJECTED（order rejected） |
| symbol       | string | BHTUSDT            | Coin pair name                                                                                                                                                                           |
| transactTime | long   | 1607702400000      | Order creation time                                                                                                                                                                      |


```json
[
    {
       "side": "BUY",
       "executedQty": 0,
       "orderId": 259396989397942275,
       "price": 10000.0000000000000000,
       "origQty": 1.0000000000000000,
       "avgPrice": 0E-8,
       "transactTime": "1607702400000",
       "action": "OPEN",
       "contractName": "E-BTC-USDT",
       "type": "LIMIT",
       "status": "INIT"
    }
]
```

## Account

Security Type: [USER\_DATA]

All interfaces under the account require​

| name                | Request type | Request url                                    | remasks                |
| ------------------- | ------------ | ---------------------------------------------- | ---------------------- |
| Account Information | get          | https://futuresopenapi.xxx.com/fapi/v1/account | Rate Limit: 20times/2s |

### Account Information
#### Parameters
***Header***
| Parameters name | data type | name         |
| --------------- | --------- | ------------ |
| X-CH-APIKEY     | string    | YOUR API-key |
| X-CH-SIGN       | string    | SIGN         |
| X-CH-TS         | integer   | TIMESTAMP    |

**Responses**
| name    | TYPE  | EXAMPLE            | DESCRIPTION |
| ------- | ----- | ------------------ | ----------- |
| account | Array | Balance collection |

***account*** field:
| name                | type   | example | description                        |
| ------------------- | ------ | ------- | ---------------------------------- |
| accountLock         | float  | 10.07   | Margin frozen account              |
| accountNormal       | float  | 10.05   | Balance account                    |
| achievedAmount      | float  | 10.07   | Profit and losses occurred         |
| marginCoin          | string | USDT    | Margin coin                        |
| partEquity          | float  | 10.07   | Restricted position equity         |
| partPositionNormal  | float  | 10.07   | Restricted position margin balance |
| positionVos         | [ ]    | ​       | Position contract record           |
| sumMarginRate       | float  | 10.07   | All accounts margin rate           |
| totalCost           | float  | 10.07   | Full position costs                |
| totalEquity         | float  | 10.07   | Full position equity               |
| totalMarginRate     | float  | 10.05   | Full position margin rate          |
| totalPositionNormal | float  | 10.07   | Full position initial margin       |
| unrealizedAmount    | float  | 10.05   | Unfilled profit and losses         |

***positionVos*** field:
| name           | type    | example    | description        |
| -------------- | ------- | ---------- | ------------------ |
| contractId     | integer | 2          | Contract id        |
| contractName   | string  | E-BTC-USDT | Contract name      |
| contractSymbol | string  | BTC-USDT   | Contract coin pair |
| positions      | Array   | ​          | Position details   |


***positions*** field:
| name                  | TYPE    | EXAMPLE | DESCRIPTION                                                               |
| --------------------- | ------- | ------- | ------------------------------------------------------------------------- |
| avgPrice              | float   | 1.05    | Hold average price                                                        |
| brokerId              | integer | 1023    | Client id                                                                 |
| capitalFee            | float   | 1.05    | Capital costs                                                             |
| closePrice            | float   | 1.05    | Balancing average price                                                   |
| closeProfit           | float   | 1.05    | Balancing profit and loss                                                 |
| closeVolume           | float   | 1.05    | Balanced quantity                                                         |
| ctime                 | time    | ​       | Creation time                                                             |
| freezeLock            | integer | 0       | Position freeze status: 0 normal, 1 liquidation freeze, 2 delivery freeze |
| historyRealizedAmount | float   | 1.05    | Historic accumulated profit and losses                                    |
| holdAmount            | float   | 1.05    | Hold position margin                                                      |
| id                    | integer | 2       | Position id                                                               |
| indexPrice            | float   | 1.05    | Newest marked price                                                       |
| keepRate              | float   | 1.05    | Scaled minimum kept margin rate                                           |
| leverageLevel         | float   | 1.05    | Leverage multiple                                                         |
| lockTime              | time    | ​       | liquidation lock time                                                     |
| marginRate            | float   | 1.05    | Margin rate                                                               |
| maxFeeRate            | float   | 1.05    | Balancing maximum fees rate                                               |
| mtime                 | time    | ​       | Update time                                                               |
| openPrice             | float   | 1.05    | Open position price                                                       |
| openRealizedAmount    | float   | 1.05    | Open position unfilled profit and losses                                  |
| pendingCloseVolume    | float   | 1.05    | The number of pending closing orders                                      |
| positionBalance       | float   | 1.05    | Position value                                                            |
| positionType          | integer | 1       | Hold position type(1 full，2 restrictive)                                 |
| realizedAmount        | float   | 1.05    | Profit and losses occurred                                                |
| reducePrice           | float   | 1.05    | Price reduction                                                           |
| returnRate            | float   | 1.05    | Return rate (profit rate)                                                 |
| shareAmount           | float   | 1.05    | Amount to share                                                           |
| side                  | string  | SELL    | Hold position direction SELL sell long, BUY buy short                     |
| status                | integer | 0       | Position effectiveness，0 ineffective 1 effective                         |
| tradeFee              | float   | 1.05    | Trading fees                                                              |
| uid                   | integer | 10023   | User ID                                                                   |
| unRealizedAmount      | float   | 1.05    | Unfilled profit and losses                                                |
| volume                | float   | 1.05    | Hold quantity                                                             |

```json
{
    "account": [
        {
            "marginCoin": "USDT",
            "accountNormal": 999.5606,
            "accountLock": 23799.5017,
            "partPositionNormal": 9110.7294,
            "totalPositionNormal": 0,
            "achievedAmount": 4156.5072,
            "unrealizedAmount": 650.6385,
            "totalMarginRate": 0,
            "totalEquity": 99964804.560,
            "partEquity": 13917.8753,
            "totalCost": 0,
            "sumMarginRate": 873.4608,
            "positionVos": [
                {
                    "contractId": 1,
                    "contractName": "E-BTC-USDT",
                    "contractSymbol": "BTC-USDT",
                    "positions": [
                        {
                            "id": 13603,
                            "uid": 10023,
                            "contractId": 1,
                            "positionType": 2,
                            "side": "BUY",
                            "volume": 69642.0,
                            "openPrice": 11840.2394,
                            "avgPrice": 11840.3095,
                            "closePrice": 12155.3005,
                            "leverageLevel": 24,
                            "holdAmount": 7014.2111,
                            "closeVolume": 40502.0,
                            "pendingCloseVolume": 0,
                            "realizedAmount": 8115.9125,
                            "historyRealizedAmount": 1865.3985,
                            "tradeFee": -432.0072,
                            "capitalFee": 2891.2281,
                            "closeProfit": 8117.6903,
                            "shareAmount": 0.1112,
                            "freezeLock": 0,
                            "status": 1,
                            "ctime": "2020-12-11T17:42:10",
                            "mtime": "2020-12-18T20:35:43",
                            "brokerId": 21,
                            "marginRate": 0.2097,
                            "reducePrice": 9740.8083,
                            "returnRate": 0.3086,
                            "unRealizedAmount": 2164.5289,
                            "openRealizedAmount": 2165.0173,
                            "positionBalance": 82458.2839,
                            "settleProfit": 0.4883,
                            "indexPrice": 12151.1175,
                            "keepRate": 0.005,
                            "maxFeeRate": 0.0025
                        }
                    ]
                }
            ]
        }
    ]
}
```