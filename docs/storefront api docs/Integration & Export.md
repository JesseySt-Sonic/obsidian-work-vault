---
tags:
  - storefront-api
---
# Integration & Export

Data feeds for external systems, punchout (cXML/Ariba), BFF passthrough, custom ERP extensions, transactional email, messaging, dealers, and warehouses.

---

## Contents

- [[#Feederdata]]
- [[#Productsrssfeed]]
- [[#Punchout]]
- [[#Bff]]
- [[#Custom]]
- [[#Messages]]
- [[#Email]]
- [[#Dealers]]
- [[#Warehouses]]

---

## Feederdata

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/feederdata/restrictionGroups/mostProducts`](#get-api-v1-feederdata-restrictiongroups-mostproducts)
- [`GET /api/v1/feederdata/customers/mostShipTos`](#get-api-v1-feederdata-customers-mostshiptos)
- [`GET /api/v1/feederdata/wishLists/mostProducts`](#get-api-v1-feederdata-wishlists-mostproducts)
- [`GET /api/v1/feederdata/product/mostWarehouses`](#get-api-v1-feederdata-product-mostwarehouses)
- [`GET /api/v1/feederdata/quickorder/products`](#get-api-v1-feederdata-quickorder-products)
- [`GET /api/v1/feederdata/brands/mostProducts`](#get-api-v1-feederdata-brands-mostproducts)

---

### `GET` /api/v1/feederdata/restrictionGroups/mostProducts

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/feederdata/customers/mostShipTos

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/feederdata/wishLists/mostProducts

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/feederdata/product/mostWarehouses

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/feederdata/quickorder/products

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `count` | integer (int32) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/feederdata/brands/mostProducts

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `startLetter` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Productsrssfeed

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/productsrssfeed`](#get-api-v1-productsrssfeed)

---

### `GET` /api/v1/productsrssfeed

**Auth required:** ❌ No

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

## Punchout

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`POST /api/v1/punchout/setuprequest`](#post-api-v1-punchout-setuprequest)
- [`GET /api/v1/punchout/sessionrequest`](#get-api-v1-punchout-sessionrequest)
- [`POST /api/v1/punchout/profiletransactionrequest`](#post-api-v1-punchout-profiletransactionrequest)
- [`GET /api/v1/punchout/porequisition`](#get-api-v1-punchout-porequisition)
- [`POST /api/v1/punchout/orderrequest`](#post-api-v1-punchout-orderrequest)

---

### `POST` /api/v1/punchout/setuprequest

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `request` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/punchout/sessionrequest

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `punchoutsessionid` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/punchout/profiletransactionrequest

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `request` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/punchout/porequisition

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `operation` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/punchout/orderrequest

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `request` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Bff

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/bff/{path}`](#get-api-v1-bff-path)
- [`PUT /api/v1/bff/{path}`](#put-api-v1-bff-path)
- [`POST /api/v1/bff/{path}`](#post-api-v1-bff-path)
- [`DELETE /api/v1/bff/{path}`](#delete-api-v1-bff-path)
- [`PATCH /api/v1/bff/{path}`](#patch-api-v1-bff-path)

---

### `GET` /api/v1/bff/{path}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `path` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `PUT` /api/v1/bff/{path}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `path` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/bff/{path}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `path` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `DELETE` /api/v1/bff/{path}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `path` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `PATCH` /api/v1/bff/{path}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `path` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/bff/{path}` | GET, PUT, POST, DELETE, PATCH |



---

## Custom

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`POST /api/v1/custom/productprice`](#post-api-v1-custom-productprice)
- [`GET /api/v1/custom/orderhistory/{webOrderNumber}/update`](#get-api-v1-custom-orderhistory-webordernumber-update)
- [`POST /api/v1/custom/customer`](#post-api-v1-custom-customer)
- [`GET /api/v1/custom/messageLog/{webOrderNumber}`](#get-api-v1-custom-messagelog-webordernumber)
- [`DELETE /api/v1/custom/messageLog/{webOrderNumber}`](#delete-api-v1-custom-messagelog-webordernumber)
- [`GET /api/v1/custom/messageLog/{webOrderNumber}/{fileName}`](#get-api-v1-custom-messagelog-webordernumber-filename)
- [`POST /api/v1/custom/finance/credit/checkCreditLimitExceed`](#post-api-v1-custom-finance-credit-checkcreditlimitexceed)
- [`GET /api/v1/custom/finance/credit/checkOverrideCreditBlock`](#get-api-v1-custom-finance-credit-checkoverridecreditblock)
- [`POST /api/v1/custom/finance/credit/overrideCreditBlock`](#post-api-v1-custom-finance-credit-overridecreditblock)
- [`GET /api/v1/custom/finance/credit/breakdown`](#get-api-v1-custom-finance-credit-breakdown)
- [`GET /api/v1/custom/countrylanguage`](#get-api-v1-custom-countrylanguage)
- [`POST /api/v1/custom/orderprocessed`](#post-api-v1-custom-orderprocessed)

---

### `POST` /api/v1/custom/productprice

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `Extensions.Controllers.ProductPriceController.RealtimePricingRequestDto`

| Property | Type | Description |
|----------|------|-------------|
| `productPriceParameters` | ProductPriceParameter[] |  |
| `warehouseId` | string | uuid |
| `billToId` | string | uuid |
| `shipToId` | string | uuid |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `Extensions.Controllers.ProductPriceController.RealtimePricingRequestDto` |

##### Response Schema: `Extensions.Controllers.ProductPriceController.RealtimePricingRequestDto`

| Property | Type | Description |
|----------|------|-------------|
| `productPriceParameters` | ProductPriceParameter[] |  |
| `warehouseId` | string | uuid |
| `billToId` | string | uuid |
| `shipToId` | string | uuid |

---

### `GET` /api/v1/custom/orderhistory/{webOrderNumber}/update

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `webOrderNumber` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `string` |

---

### `POST` /api/v1/custom/customer

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `Extensions.Models.DTO.CustomerBillToDto`

| Property | Type | Description |
|----------|------|-------------|
| `warehouseId` | string | uuid |
| `currencyId` | string | uuid |
| `vatNumber` | string |  |
| `priceCode` | string |  |
| `termsCode` | string |  |
| `deliveryConditionIstia` | string |  |
| `deliveryConditionIstiaPickup` | string |  |
| `incoTerms` | string |  |
| `industry` | string |  |
| `invoiceLanguageId` | string |  |
| `emailAdministration` | string |  |
| `id` | string | uuid |
| `parentId` | string | uuid |
| `customerNumber` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `postalCode` | string |  |
| `city` | string |  |
| `countryId` | string | uuid |
| `email` | string |  |
| `phone` | string |  |
| `multiversAdministrationId` | string |  |
| `isBillTo` | boolean |  |
| `isShipTo` | boolean |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/custom/messageLog/{webOrderNumber}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `webOrderNumber` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `DELETE` /api/v1/custom/messageLog/{webOrderNumber}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `webOrderNumber` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/custom/messageLog/{webOrderNumber}/{fileName}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `webOrderNumber` | string | ✅ |  |
| `fileName` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/custom/finance/credit/checkCreditLimitExceed

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `Extensions.Integrations.Finance.Models.CreditExceedCheckRequest`

| Property | Type | Description |
|----------|------|-------------|
| `customerId` | string | uuid |
| `orderAdjustmentDelta` | number | decimal |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/custom/finance/credit/checkOverrideCreditBlock

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `webOrderNumber` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/custom/finance/credit/overrideCreditBlock

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `Extensions.Integrations.Finance.Models.CreditBlockOverrideRequest`

| Property | Type | Description |
|----------|------|-------------|
| `webOrderNumber` | string |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/custom/finance/credit/breakdown

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `customerId` | string (uuid) | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/custom/countrylanguage

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `POST` /api/v1/custom/orderprocessed

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `Extensions.Integrations.Warehouse.Models.DTO.IstiaResponse`

| Property | Type | Description |
|----------|------|-------------|
| `status` | integer | int32 |
| `message` | string |  |
| `request` | Extensions.Integrations.Warehouse.Models.DTO.OrderRequest |  |
| `exceptionMessage` | string |  |
| `stackTrace` | string |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/custom/messageLog/{webOrderNumber}` | GET, DELETE |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/custom/messageLog/{webOrderNumber}`

**Child / sub-resources:**

- `/api/v1/custom/messageLog/{webOrderNumber}/{fileName}`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{webOrderNumber}`

**Linked paths:**

- `/api/v1/custom/messageLog/{webOrderNumber}`
- `/api/v1/custom/messageLog/{webOrderNumber}/{fileName}`
- `/api/v1/custom/orderhistory/{webOrderNumber}/update`



---

## Messages

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/messages`](#get-api-v1-messages)
- [`POST /api/v1/messages`](#post-api-v1-messages)
- [`GET /api/v1/messages/{messageId}`](#get-api-v1-messages-messageid)
- [`PATCH /api/v1/messages/{messageId}`](#patch-api-v1-messages-messageid)

---

### `GET` /api/v1/messages

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `MessageCollectionModel` |

##### Response Schema: `MessageCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `messages` | MessageModel[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/messages

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `MessageParameter`

| Property | Type | Description |
|----------|------|-------------|
| `customerOrderId` | string | uuid |
| `toUserProfileId` | string | uuid |
| `subject` | string |  |
| `message` | string |  |
| `process` | string |  |
| `toUserProfileName` | string |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `MessageModel` |

##### Response Schema: `MessageModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `body` | string |  |
| `subject` | string |  |
| `dateToDisplay` | string | date-time |
| `isRead` | boolean |  |
| `displayName` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/messages/{messageId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `messageId` | string (uuid) | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `MessageModel` |

##### Response Schema: `MessageModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `body` | string |  |
| `subject` | string |  |
| `dateToDisplay` | string | date-time |
| `isRead` | boolean |  |
| `displayName` | string |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/messages/{messageId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `messageId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `MessageModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `body` | string |  |
| `subject` | string |  |
| `dateToDisplay` | string | date-time |
| `isRead` | boolean |  |
| `displayName` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `MessageModel` |

##### Response Schema: `MessageModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `body` | string |  |
| `subject` | string |  |
| `dateToDisplay` | string | date-time |
| `isRead` | boolean |  |
| `displayName` | string |  |
| `properties` | object |  |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/messages` | GET, POST |
| `/api/v1/messages/{messageId}` | GET, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/messages`

**Child / sub-resources:**

- `/api/v1/messages/{messageId}`



---

## Email

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/email`](#get-api-v1-email)
- [`POST /api/v1/email/tellafriend`](#post-api-v1-email-tellafriend)
- [`POST /api/v1/email/contactUs`](#post-api-v1-email-contactus)

---

### `GET` /api/v1/email

**Auth required:** ❌ No

**Accept:** application/json, text/json, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `System.Web.Http.Results.OkResult` |

##### Response Schema: `System.Web.Http.Results.OkResult`

| Property | Type | Description |
|----------|------|-------------|
| `request` | string |  |

---

### `POST` /api/v1/email/tellafriend

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `TellAFriendModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `friendsName` | string |  |
| `friendsEmailAddress` | string |  |
| `yourName` | string |  |
| `yourEmailAddress` | string |  |
| `yourMessage` | string |  |
| `productId` | string |  |
| `productImage` | string |  |
| `productShortDescription` | string |  |
| `altText` | string |  |
| `productUrl` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `TellAFriendModel` |

##### Response Schema: `TellAFriendModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `friendsName` | string |  |
| `friendsEmailAddress` | string |  |
| `yourName` | string |  |
| `yourEmailAddress` | string |  |
| `yourMessage` | string |  |
| `productId` | string |  |
| `productImage` | string |  |
| `productShortDescription` | string |  |
| `altText` | string |  |
| `productUrl` | string |  |
| `properties` | object |  |

---

### `POST` /api/v1/email/contactUs

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `ContactUsModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `message` | string |  |
| `topic` | string |  |
| `phoneNumber` | string |  |
| `emailAddress` | string |  |
| `emailTo` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ContactUsModel` |

##### Response Schema: `ContactUsModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `message` | string |  |
| `topic` | string |  |
| `phoneNumber` | string |  |
| `emailAddress` | string |  |
| `emailTo` | string |  |
| `properties` | object |  |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/email`

**Child / sub-resources:**

- `/api/v1/email/contactUs`
- `/api/v1/email/tellafriend`



---

## Dealers

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/dealers`](#get-api-v1-dealers)
- [`GET /api/v1/dealers/{dealerId}`](#get-api-v1-dealers-dealerid)

---

### `GET` /api/v1/dealers

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.useDefaultLocation` | boolean | ❌ |  |
| `parameter.latitude` | number (double) | ❌ |  |
| `parameter.longitude` | number (double) | ❌ |  |
| `parameter.radius` | integer (int32) | ❌ |  |
| `parameter.name` | string | ❌ |  |
| `parameter.startPage` | integer (int32) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `DealerCollectionModel` |

##### Response Schema: `DealerCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `dealers` | DealerModel[] |  |
| `distanceUnitOfMeasure` | string |  |
| `pagination` | PaginationModel |  |
| `defaultLatitude` | number | double |
| `defaultLongitude` | number | double |
| `formattedAddress` | string |  |
| `defaultRadius` | integer | int32 |
| `startDealerNumber` | integer | int32 |
| `properties` | object |  |

---

### `GET` /api/v1/dealers/{dealerId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `dealerId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `DealerModel` |

##### Response Schema: `DealerModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `city` | string |  |
| `state` | string |  |
| `postalCode` | string |  |
| `countryId` | string | uuid |
| `phone` | string |  |
| `fax` | string |  |
| `manager` | string |  |
| `latitude` | number | decimal |
| `longitude` | number | decimal |
| `webSiteUrl` | string |  |
| `htmlContent` | string |  |
| `distance` | number | double |
| `distanceUnitOfMeasure` | string |  |
| `properties` | object |  |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/dealers`

**Child / sub-resources:**

- `/api/v1/dealers/{dealerId}`



---

## Warehouses

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/warehouses`](#get-api-v1-warehouses)
- [`GET /api/v1/warehouses/{warehouseId}`](#get-api-v1-warehouses-warehouseid)

---

### `GET` /api/v1/warehouses

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.sort` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.expand` | string | ❌ |  |
| `parameter.onlyPickupWarehouses` | boolean | ❌ |  |
| `parameter.useDefaultLocation` | boolean | ❌ |  |
| `parameter.latitude` | number (double) | ❌ |  |
| `parameter.longitude` | number (double) | ❌ |  |
| `parameter.radius` | integer (int32) | ❌ |  |
| `parameter.excludeCurrentPickupWarehouse` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WarehouseCollectionModel` |

##### Response Schema: `WarehouseCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `warehouses` | WarehouseModel[] |  |
| `pagination` | PaginationModel |  |
| `distanceUnitOfMeasure` | string |  |
| `defaultLatitude` | number | double |
| `defaultLongitude` | number | double |
| `defaultRadius` | integer | int32 |
| `properties` | object |  |

---

### `GET` /api/v1/warehouses/{warehouseId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `warehouseId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WarehouseModel` |

##### Response Schema: `WarehouseModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `city` | string |  |
| `contactName` | string |  |
| `countryId` | string | uuid |
| `deactivateOn` | string | date-time |
| `description` | string |  |
| `phone` | string |  |
| `postalCode` | string |  |
| `shipSite` | string |  |
| `state` | string |  |
| `isDefault` | boolean |  |
| `alternateWarehouses` | WarehouseModel[] |  |
| `latitude` | number | decimal |
| `longitude` | number | decimal |
| `hours` | string |  |
| `distance` | number | double |
| `allowPickup` | boolean |  |
| `pickupShipViaId` | string | uuid |
| `properties` | object |  |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/warehouses`

**Child / sub-resources:**

- `/api/v1/warehouses/{warehouseId}`



---

