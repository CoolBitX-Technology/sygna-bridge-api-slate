---
title: Sygna API Spec

language_tabs: # must be one of https://git.io/vQNgJ


toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

The Sygna API allows you to validate the source or recipient of a Blockchain transaction. Based on Slate.

**API METHODS:**

_**`GET`**_   
- **getAddressStatus** - Queries the status of an address (ex: External, Whitelisted, Banned, Restricted, ...) 

_**`POST`**_  
- **SygnaAddress** -  Generates a Sygna-Certified address for a user who has already been KYC'd.    
- **addUser** - Adds a user to the Sygna whitelist - requires the User to have already gone through the exchange KYC  
- **linkAddress**  - Links an existing Address to an existing Sygna UserID. (Individual Addresses have to be linked to KYC identities)

<aside class="success">
Note — (API <b>not currently active</b> as it is being worked on)
</aside>

#Request URLs
Test requests should use the following endpoint:  
`https://test.sygna.com/api/syg/v1`

Production server URL for the API is located at:  
`https://api.sygna.com/api/syg/v1`

# Authentication
We are using `OAuth 2.0` for Authentication. 

# Users

## Add User

Adds a user to the Sygna whitelist - requires the User to have already gone through the exchange KYC

### HTTP Request
> Request Body

```json

  {
      "exchangeUserId": <string>,
      "name": <string>,
      "email": <string>
  }

```

**`POST`**`https://api.sygna.com/api/syg/v1/users/`

### Request Parameters


| Parameter      | Description                  |
| -------------- | ---------------------------- |
| exchangeUserId | The user id in your exchange |
| name           | User name                    |
| email          | User email                   |

### Response Parameters
> Response Body

```json

  {
      "sygnaUserId": <string>
  }

```

| Parameter   | Description          |
| ----------- | -------------------- |
| sygnaUserId | The user id in Sygna |

<aside class="success">
Remember — A user first has to be added before his addresses can be Sygna-Certified
</aside>

## SygnaAddress

Requests an existing SygnaWallet Address (for existing Sygna user). The user must have a Sygna Wallet and activated it. (NB: in a SygnaWallet, Sygna acts as the custodian of the private keys)

_usage_: fetches exchisting SygnaWallet Address

### HTTP Request

**`GET`**`https://api.sygna.com/api/syg/v1/users/{sygnaUserId}/{coinType}/`

### URL Parameters

| Parameter | Description                               |
| --------- | ----------------------------------------- |
| sygnaUserId | The user id in Sygna                      |
| coinType  | Crypto address format (BTC/ETH/BCH)       |

### Response Body
> Response Body

```json
{
  "sygnaAddress": <string>
}
```

| Parameter    | Description                      |
| ------------ | -------------------------------- |
| sygnaAddress | New Sygna address for that user  |


## Link Address

> Request Body

```json

  {
      "userAddress": <string>
  }

```

Links an existing Address to an existing Sygna UserID.

### HTTP Request

**`POST`**`https://api.sygna.com/api/syg/v1/users/{sygnaUserId}/{coinType}/`

### URL Parameters

| Parameter | Description          |
| --------- | -------------------- |
| sygnaUserId    | The user id in Sygna |

### Request Body

| Parameter       | Description                               |
| --------------- | ----------------------------------------- |
| exchangeAddress | The address from exchange wallet          |

###

# Address

## Get Address Status



When you want to query the status of an address

### HTTP Request

**`GET`**`https://api.sygna.com/api/syg/v1/addresses/{address}/status`

### Response Body
> Response Body

```json
{
   "status": "External|Whitelisted|Banned|Restricted"
}
```

| Parameter | Description               |
| --------- | ------------------------- |
| status    | The status of the address |
