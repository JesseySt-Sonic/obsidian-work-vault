---
tags:
  - storefront-api
---
# Payment

Payment gateway configuration, authentication flows, and tokenisation. Adyen, Paymetric, Spreedly, and TokenEx are interchangeable provider adapters behind the `paymentauthentication` facade.

---

## Contents

- [[#Paymentauthentication]]
- [[#Adyen]]
- [[#Paymetric]]
- [[#Spreedly]]
- [[#Tokenexconfig]]

---

## Paymentauthentication

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`POST /api/v1/paymentauthentication`](#post-api-v1-paymentauthentication)
- [`POST /api/v1/paymentauthentication/threedsnotify`](#post-api-v1-paymentauthentication-threedsnotify)
- [`POST /api/v1/paymentauthentication/adyenwebhook`](#post-api-v1-paymentauthentication-adyenwebhook)
- [`POST /api/v1/paymentauthentication/adyenpaymentdetails`](#post-api-v1-paymentauthentication-adyenpaymentdetails)
- [`POST /api/v1/paymentauthentication/adyenpayment`](#post-api-v1-paymentauthentication-adyenpayment)
- [`POST /api/v1/paymentauthentication/adyenrefund`](#post-api-v1-paymentauthentication-adyenrefund)
- [`POST /api/v1/paymentauthentication/threedschallengeresponse`](#post-api-v1-paymentauthentication-threedschallengeresponse)
- [`POST /api/v1/paymentauthentication/threedscallback`](#post-api-v1-paymentauthentication-threedscallback)

---

### `POST` /api/v1/paymentauthentication

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, text/html

#### Request Body

**Schema:** `PaymentAuthenticationParameter`

| Property | Type | Description |
|----------|------|-------------|
| `currency` | string |  |
| `transactionId` | string |  |
| `cardNumber` | string |  |
| `expirationMonth` | integer | int32 |
| `expirationYear` | integer | int32 |
| `orderAmount` | string |  |
| `operation` | string |  |
| `returnUrl` | string |  |
| `cartId` | string | uuid |
| `isPaymentProfile` | boolean |  |
| `webOrderNumber` | string |  |
| `resume3Ds` | boolean |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `PaymentAuthenticationModel` |

##### Response Schema: `PaymentAuthenticationModel`

| Property | Type | Description |
|----------|------|-------------|
| `transactionId` | string |  |
| `webOrderNumber` | string |  |
| `threeDs` | ThreeDsDto |  |
| `sessionData` | string |  |
| `action` | string |  |
| `region` | string |  |

---

### `POST` /api/v1/paymentauthentication/threedsnotify

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `object`

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/paymentauthentication/adyenwebhook

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `AdyenWebhook.WebhookModel`

| Property | Type | Description |
|----------|------|-------------|
| `notificationItems` | AdyenWebhook.NotificationItemModel[] |  |
| `live` | boolean |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/paymentauthentication/adyenpaymentdetails

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `AdyenPaymentDetails.PaymentDetailsRequest`

| Property | Type | Description |
|----------|------|-------------|
| `details` | AdyenPaymentDetails.Details |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/paymentauthentication/adyenpayment

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `object`

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/paymentauthentication/adyenrefund

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `AdyenRefundParameter`

| Property | Type | Description |
|----------|------|-------------|
| `pspReference` | string |  |
| `orderNumber` | string |  |
| `amount` | AdyenWebhook.AmountModel |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/paymentauthentication/threedschallengeresponse

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `object`

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ThreeDsChallengeResult` |

##### Response Schema: `ThreeDsChallengeResult`

| Property | Type | Description |
|----------|------|-------------|
| `messageId` | string |  |
| `threeDSServerTransID` | string | uuid |
| `valid` | boolean |  |
| `rReq` | ThreeDSChallengeRreq |  |

---

### `POST` /api/v1/paymentauthentication/threedscallback

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/paymentauthentication`

**Child / sub-resources:**

- `/api/v1/paymentauthentication/adyenpayment`
- `/api/v1/paymentauthentication/adyenpaymentdetails`
- `/api/v1/paymentauthentication/adyenrefund`
- `/api/v1/paymentauthentication/adyenwebhook`
- `/api/v1/paymentauthentication/threedscallback`
- `/api/v1/paymentauthentication/threedschallengeresponse`
- `/api/v1/paymentauthentication/threedsnotify`



---

## Adyen

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/adyen/config`](#get-api-v1-adyen-config)

---

### `GET` /api/v1/adyen/config

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Paymetric

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`POST /api/v1/paymetric/config`](#post-api-v1-paymetric-config)
- [`GET /api/v1/paymetric/responsepacket`](#get-api-v1-paymetric-responsepacket)

---

### `POST` /api/v1/paymetric/config

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/paymetric/responsepacket

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `accessToken` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Spreedly

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/spreedly/config`](#get-api-v1-spreedly-config)

---

### `GET` /api/v1/spreedly/config

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Tokenexconfig

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/tokenexconfig`](#get-api-v1-tokenexconfig)

---

### `GET` /api/v1/tokenexconfig

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `token` | string | ❌ |  |
| `isECheck` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

