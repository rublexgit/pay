# Rublex Payment Gateway API Documentation

## Guide to APIs:
Documentation for all services provided in the Rublex Payment Gateway is prepared separately, specifying the input parameters and possible outputs under successful request processing conditions or possible errors.

However, descriptions of the most commonly used online payment gateway services are provided below. To use these APIs, it is necessary to first create your own dedicated store on the Rublex payment website at the following address and receive your terminal token:

[https://panel.pay.rublex.io](https://panel.pay.rublex.io)

For the following APIs, it is necessary to include the terminal token in the headers of the sent requests with the name "Token".

### Retrieve Terminal Information
```
curl --location 'https://panel.pay.rublex.io/terminals/v1/info' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Token: <Terminal Token>'
```
```
Inputs: None
``` 
```
Outputs:
   "status": "SUCCESS",
   "message": "request.successful",
   "data": {
       "store_name": "<Store Name>",
       "name": "<Terminal Name>",
       "ip": "<Terminal IP Address>",
       "description": "<Terminal Description>",
       "is_locked": "<Whether the terminal is locked or not>",
       "lock_reason": "<Reason for terminal being locked>"
     }
```

### Get Complete List of System Currencies
```
curl --location 'https://panel.pay.rublex.io/terminals/v1/currencies' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Token: <Terminal Token>'
```
```
Inputs: None
``` 
```
Outputs:
  "status": "SUCCESS",
  "message": "request.successful",
  "data": [
      {
          "id": "<Currency ID>",
          "coin_market_cap_id": "<Currency ID in Coin Market Cap>",
          "title": "<Token and Coin Network Title>",
          "image": "<Currency Icon>",
          "current_price": "<Currency Current Price>"
      },
      ...
  ]
```

### Get List of Supported Currencies by Personal Terminal
```
Inputs: None
``` 
```
Outputs:
  "status": "SUCCESS",
  "message": "request.successful",
  "data": [
      {
          "id": "<Currency ID>",
          "coin_market_cap_id": "<Currency ID in Coin Market Cap>",
          "title": "<Token and Coin Network Title>",
          "image": "<Currency Icon>",
          "current_price": "<Currency Current Price>"
      },
      ...
  ]
```
```
curl --location 'https://panel.pay.rublex.io/terminals/v1/currencies/supported' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Token: <Terminal Token>'
```


### Payment Request (Invoice Creation) by Merchant
```
Inputs:
  - "amount": "<Invoice Amount>",
  - "currency_id": "<Payment Currency ID>",
  - "callback_url": "<URL to be called upon Invoice status change>"
```
```
Outputs:
  "status": "SUCCESS",
  "message": "request.successful",
  "data": {
      "invoice_number": "<Invoice Number>",
      "customer_email": "<Payer's Email>",
      "payment_address": "<Wallet Address for Payment>",
      "currency": "<Payment Currency>",
      "amount": "<Invoice Amount>",
      "paid_amount": "<Amount Paid until Now>",
      "status": "<Invoice Status>",
      "invoice_url": "<URL for Invoice Status Inquiry>"
  }
```
```
curl --location 'https://panel.pay.rublex.io/terminals/v1/pay-request' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Token: <Terminal Token>' \
--data '{
    "amount": <Invoice Amount>,
    "currency_id": <Payment Currency ID>,
    "callback_url": "<URL to be called upon Invoice status change>"
}'
```


### Retrieve Invoice Status
```
Inputs: None
```
```
Outputs:
  "status": "SUCCESS",
  "message": "request.successful",
  "data": {
      "invoice_number": "<Invoice Number>",
      "customer_email": "<Payer's Email>",
      "payment_address": "<Wallet Address for Payment>",
      "currency": "<Payment Currency>",
      "amount": "<Invoice Amount>",
      "paid_amount": "<Amount Paid until Now>",
      "status": "<Invoice Status>",
      "invoice_url": "<URL for Invoice Status Inquiry>"
  }
```
```
curl --location 'https://panel.pay.rublex.io/terminals/v1/invoices?invoice_number=<Invoice Number>' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Token: <Terminal Token>'
```

### Retrieve List of Financial Transactions
```
Inputs: None
```
```
Outputs:
  "status": "SUCCESS",
  "message": "request.successful",
  "data": [
      {
          "invoice_number": "<Invoice Number>",
          "customer_email": "<Payer's Email>",
          "payment_address": "<Wallet Address for Payment>",
          "currency": "<Payment Currency>",
          "amount": "<Invoice Amount>",
          "paid_amount": "<Amount Paid until Now>",
          "status": "<Invoice Status>",
          "invoice_url": "<URL for Invoice Status Inquiry>"
      },
      ...
  ]
```
```
curl --location 'https://panel.pay.rublex.io/terminals/v1/transactions' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Token: <Terminal Token>'
```
