---
title: Sygna API Spec

language_tabs: # must be one of https://git.io/vQNgJ


toc_footers:
  - <a href='https://coolwallet.io/contact/'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

The Sygna API allows you to validate the source or recipient of a Blockchain transaction.

**API METHODS:**

_**`GET`**_   
- **Sygna Address** -  fetches an existing Sygna-Certified address for a user who has already been KYC'd  
- **Address Status** - Queries the status of an address (ex: External, Whitelisted, Banned, Restricted, ...)   

_**`POST`**_  
- **Link Address**  - Links an existing Address to an existing Sygna UserID. (Individual Addresses have to be linked to KYC identities)

<aside class="success">
Note — (API <b>not currently active</b> as it is being worked on)
</aside>

#Request URLs
Test requests should use the following endpoint:  
`https://test.sygna.com/api/syg/v1`

Production server URL for the API is located at:  
`https://api.sygna.com/api/syg/v1`

# Authentication

[Documentation] (https://hackmd.io/s/H1zZ4F6cV)

1. The third party platform could exchange the user id for sygna user reference id via Sygna SSO login.

2. Sign in for one time and using everywhere.

# Users

## Sygna Address

Requests an existing SygnaWallet Address (for existing Sygna user). The user must have a Sygna Wallet and activated it. (NB: in a SygnaWallet, Sygna acts as the custodian of the private keys)

_usage_: fetches exchisting SygnaWallet Address

### HTTP Request

**`GET`**`https://api.sygna.com/api/syg/v1/users/{sygnaUserId}?coinType={coinType}`

### URL Parameters

| Parameter | Description                               |
| --------- | ----------------------------------------- |
| sygnaUserId | The user id in Sygna                    |
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

**`POST`**`https://api.sygna.com/api/syg/v1/users/{sygnaUserId}`

### URL Parameters

| Parameter | Description          |
| --------- | -------------------- |
| sygnaUserId    | The user id in Sygna |

### Request Body

| Parameter       | Description                               |
| --------------- | ----------------------------------------- |
| exchangeAddress | The address from exchange wallet          |
| coinType        | Crypto address format (BTC/ETH/BCH)       |

###

# Address

## Address Status


When you want to query the status of an address

### HTTP Request

**`GET`**`https://api.sygna.com/api/syg/v1/addresses/{address}?q=status`

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

