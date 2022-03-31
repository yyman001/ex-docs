# Errors
>Error code explanation

Errors consist of two parts: an error code and a message. Codes are universal, but messages can vary. Here is the error JSON payload:

```js
{
  "code": -1121,
  "msg": "Invalid symbol."
}
```

## 10xx - General Server or Network issues

### -1000 UNKNOWN

*   An unknown error occured while processing the request.

### -1001 DISCONNECTED

*   Internal error; unable to process your request. Please try again.

### -1002 UNAUTHORIZED

*   You are not authorized to execute this request. Request need API Key included in . We suggest that API Key be included in any request.

### -1003 TOO_MANY_REQUESTS

*   Requests exceed the limit too frequently.

### -1004 NO_THIS_COMPANY

*   You are not authorized to execute this request. User not exit Company

### -1006 UNEXPECTED_RESP

*   An unexpected response was received from the message bus. Execution status unknown. OPEN API server find some exception in execute request .Please report to Customer service.

### -1007 TIMEOUT

*   Timeout waiting for response from backend server. Send status unknown; execution status unknown.

### -1014 UNKNOWN_ORDER_COMPOSITION

*   Unsupported order combination.

### -1015 TOO_MANY_ORDERS

*   Too many new orders.

### -1016 SERVICE_SHUTTING_DOWN

*   This service is no longer available.

### -1017 ILLEGAL_CONTENT_TYPE

*   We recommend attaching Content-Type to all request headers and setting it to application/json

### -1020 UNSUPPORTED_OPERATION

*   This operation is not supported.

### -1021 INVALID_TIMESTAMP

*   Timestamp for this request is outside of the recvWindow.

*   Timestamp for this request was 1000ms ahead of the server's time.

*   Please check the difference between your local time and server time .

### -1022 INVALID_SIGNATURE

*   Signature for this request is not valid.

### -1023 UNTIMESTAMP

*   You are not authorized to execute this request, we recommend that you add X-CH-TS to all request headers

### -1024 UNSIGNATURE

*   You are not authorized to execute this request, we recommend that you add X-CH-SIGN to the request header

## 11xx - Request issues

### -1100 ILLEGAL_CHARS

*   Illegal characters found in a parameter.

### -1101 TOO_MANY_PARAMETERS

*   Too many parameters sent for this endpoint.

### -1102 MANDATORY_PARAM_EMPTY_OR_MALFORMED

*   A mandatory parameter was not sent, was empty/null, or malformed.

*   Mandatory parameter '%s' was not sent, was empty/null, or malformed.

*   Param '%s' or '%s' must be sent, but both were empty/null!

### -1103 UNKNOWN_PARAM

*   An unknown parameter was sent.

*   each request requires at least one parameter. {Timestamp}.

### -1104 UNREAD_PARAMETERS

*   Not all sent parameters were read.

*   Not all sent parameters were read; read '%s' parameter(s) but was sent '%s'.

### -1105 PARAM_EMPTY

*   A parameter was empty.

*   Parameter '%s' was empty.

### -1106 PARAM_NOT_REQUIRED

*   A parameter was sent when not required.

*   Parameter '%s' sent when not required.

### -1111 BAD_PRECISION

*   Precision is over the maximum defined for this asset.

### -1112 NO_DEPTH

*   No orders on book for symbol.

### -1116 INVALID_ORDER_TYPE

*   Invalid orderType.

*   In the current version , ORDER_TYPE values is LIMIT or MARKET.

### -1117 INVALID_SIDE

*   Invalid side.

*   ORDER_SIDE values is BUY or SELL

### -1118 EMPTY_NEW_CL_ORD_ID

*   New client order ID was empty.

### -1121 BAD_SYMBOL

*   Invalid symbol.

### -1136 ORDER_VOLUME_TOO_SMALL

*   Order volume lower than the minimum.

### -1138 ORDER_PRICE_WAVE_EXCEED

*   Order price exceeds permissible range.

### -1139 ORDER_NOT_SUPPORT_MARKET

*   This trading pair does not support market trading

### -1145 ORDER_NOT_SUPPORT_CANCELLATION

*   This order type does not support cancellation

### -2013 NO_SUCH_ORDER

*   Order does not exist.

### -2015 REJECTED_CH_KEY

*   Invalid API-key, IP, or permissions for action.

### -2016 EXCHANGE_LOCK

*   Transaction is frozen

### -2017 BALANCE_NOT_ENOUGH

*   Insufficient balance
