---
tags:
  - storefront-api
---
# Identity & Account

Manages user identity, session lifecycle, billing/shipping addresses, and saved payment profiles. This is the foundation layer — all authenticated requests depend on the `access_token` produced here.

---

## Contents

- [[#Accounts]]
- [[#Sessions]]
- [[#Billtos]]

---

## Accounts

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`PATCH /api/v1/accounts/{accountId}/shiptos`](#patch-api-v1-accounts-accountid-shiptos)
- [`GET /api/v1/accounts`](#get-api-v1-accounts)
- [`POST /api/v1/accounts`](#post-api-v1-accounts)
- [`GET /api/v1/accounts/{accountId}`](#get-api-v1-accounts-accountid)
- [`PATCH /api/v1/accounts/{accountId}`](#patch-api-v1-accounts-accountid)
- [`POST /api/v1/accounts/vmi/import`](#post-api-v1-accounts-vmi-import)
- [`PATCH /api/v1/accounts/vmi/{vmiUserId}`](#patch-api-v1-accounts-vmi-vmiuserid)
- [`GET /api/v1/accounts/current/paymentprofiles`](#get-api-v1-accounts-current-paymentprofiles)
- [`POST /api/v1/accounts/current/paymentprofiles`](#post-api-v1-accounts-current-paymentprofiles)
- [`GET /api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}`](#get-api-v1-accounts-current-paymentprofiles-accountpaymentprofileid)
- [`DELETE /api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}`](#delete-api-v1-accounts-current-paymentprofiles-accountpaymentprofileid)
- [`PATCH /api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}`](#patch-api-v1-accounts-current-paymentprofiles-accountpaymentprofileid)

---

### `PATCH` /api/v1/accounts/{accountId}/shiptos

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `accountId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `AccountShipToCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `userShipToCollection` | AccountShipToModel[] |  |
| `costCodeCollection` | CustomerCostCodeDto[] |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountShipToCollectionModel` |

##### Response Schema: `AccountShipToCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `userShipToCollection` | AccountShipToModel[] |  |
| `costCodeCollection` | CustomerCostCodeDto[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/accounts

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.expand` | string | ❌ |  |
| `parameter.searchText` | string | ❌ |  |
| `parameter.startPage` | integer (int32) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.roles` | string[] | ❌ |  |
| `parameter.excludeRoles` | string[] | ❌ |  |
| `parameter.userNames` | string[] | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountCollectionModel` |

##### Response Schema: `AccountCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `accounts` | AccountModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `POST` /api/v1/accounts

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `AccountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `email` | string |  |
| `userName` | string |  |
| `password` | string |  |
| `isSubscribed` | boolean |  |
| `isGuest` | boolean |  |
| `canApproveOrders` | boolean |  |
| `canViewApprovalOrders` | boolean |  |
| `billToId` | string | uuid |
| `shipToId` | string | uuid |
| `firstName` | string |  |
| `lastName` | string |  |
| `role` | string |  |
| `roleTranslated` | string |  |
| `vmiRole` | string |  |
| `vmiRoleTranslated` | string |  |
| `approver` | string |  |
| `isApproved` | boolean |  |
| `activationStatus` | string |  |
| `lastLoginOn` | string | date-time |
| `availableApprovers` | string[] |  |
| `availableRoles` | string[] |  |
| `availableRolesTranslated` | object |  |
| `requiresActivation` | boolean |  |
| `setDefaultCustomer` | boolean |  |
| `defaultCustomerId` | string | uuid |
| `defaultFulfillmentMethod` | string |  |
| `defaultWarehouseId` | string | uuid |
| `defaultWarehouse` | WarehouseModel |  |
| `accessToken` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountModel` |

##### Response Schema: `AccountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `email` | string |  |
| `userName` | string |  |
| `password` | string |  |
| `isSubscribed` | boolean |  |
| `isGuest` | boolean |  |
| `canApproveOrders` | boolean |  |
| `canViewApprovalOrders` | boolean |  |
| `billToId` | string | uuid |
| `shipToId` | string | uuid |
| `firstName` | string |  |
| `lastName` | string |  |
| `role` | string |  |
| `roleTranslated` | string |  |
| `vmiRole` | string |  |
| `vmiRoleTranslated` | string |  |
| `approver` | string |  |
| `isApproved` | boolean |  |
| `activationStatus` | string |  |
| `lastLoginOn` | string | date-time |
| `availableApprovers` | string[] |  |
| `availableRoles` | string[] |  |
| `availableRolesTranslated` | object |  |
| `requiresActivation` | boolean |  |
| `setDefaultCustomer` | boolean |  |
| `defaultCustomerId` | string | uuid |
| `defaultFulfillmentMethod` | string |  |
| `defaultWarehouseId` | string | uuid |
| `defaultWarehouse` | WarehouseModel |  |
| `accessToken` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/accounts/{accountId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `accountId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountModel` |

##### Response Schema: `AccountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `email` | string |  |
| `userName` | string |  |
| `password` | string |  |
| `isSubscribed` | boolean |  |
| `isGuest` | boolean |  |
| `canApproveOrders` | boolean |  |
| `canViewApprovalOrders` | boolean |  |
| `billToId` | string | uuid |
| `shipToId` | string | uuid |
| `firstName` | string |  |
| `lastName` | string |  |
| `role` | string |  |
| `roleTranslated` | string |  |
| `vmiRole` | string |  |
| `vmiRoleTranslated` | string |  |
| `approver` | string |  |
| `isApproved` | boolean |  |
| `activationStatus` | string |  |
| `lastLoginOn` | string | date-time |
| `availableApprovers` | string[] |  |
| `availableRoles` | string[] |  |
| `availableRolesTranslated` | object |  |
| `requiresActivation` | boolean |  |
| `setDefaultCustomer` | boolean |  |
| `defaultCustomerId` | string | uuid |
| `defaultFulfillmentMethod` | string |  |
| `defaultWarehouseId` | string | uuid |
| `defaultWarehouse` | WarehouseModel |  |
| `accessToken` | string |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/accounts/{accountId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `accountId` | string | ✅ |  |

#### Request Body

**Schema:** `AccountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `email` | string |  |
| `userName` | string |  |
| `password` | string |  |
| `isSubscribed` | boolean |  |
| `isGuest` | boolean |  |
| `canApproveOrders` | boolean |  |
| `canViewApprovalOrders` | boolean |  |
| `billToId` | string | uuid |
| `shipToId` | string | uuid |
| `firstName` | string |  |
| `lastName` | string |  |
| `role` | string |  |
| `roleTranslated` | string |  |
| `vmiRole` | string |  |
| `vmiRoleTranslated` | string |  |
| `approver` | string |  |
| `isApproved` | boolean |  |
| `activationStatus` | string |  |
| `lastLoginOn` | string | date-time |
| `availableApprovers` | string[] |  |
| `availableRoles` | string[] |  |
| `availableRolesTranslated` | object |  |
| `requiresActivation` | boolean |  |
| `setDefaultCustomer` | boolean |  |
| `defaultCustomerId` | string | uuid |
| `defaultFulfillmentMethod` | string |  |
| `defaultWarehouseId` | string | uuid |
| `defaultWarehouse` | WarehouseModel |  |
| `accessToken` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountModel` |

##### Response Schema: `AccountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `email` | string |  |
| `userName` | string |  |
| `password` | string |  |
| `isSubscribed` | boolean |  |
| `isGuest` | boolean |  |
| `canApproveOrders` | boolean |  |
| `canViewApprovalOrders` | boolean |  |
| `billToId` | string | uuid |
| `shipToId` | string | uuid |
| `firstName` | string |  |
| `lastName` | string |  |
| `role` | string |  |
| `roleTranslated` | string |  |
| `vmiRole` | string |  |
| `vmiRoleTranslated` | string |  |
| `approver` | string |  |
| `isApproved` | boolean |  |
| `activationStatus` | string |  |
| `lastLoginOn` | string | date-time |
| `availableApprovers` | string[] |  |
| `availableRoles` | string[] |  |
| `availableRolesTranslated` | object |  |
| `requiresActivation` | boolean |  |
| `setDefaultCustomer` | boolean |  |
| `defaultCustomerId` | string | uuid |
| `defaultFulfillmentMethod` | string |  |
| `defaultWarehouseId` | string | uuid |
| `defaultWarehouse` | WarehouseModel |  |
| `accessToken` | string |  |
| `properties` | object |  |

---

### `POST` /api/v1/accounts/vmi/import

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `VmiUserImportCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `vmiUsers` | VmiUserImportModel[] |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiUserImportCollectionModel` |

##### Response Schema: `VmiUserImportCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `vmiUsers` | VmiUserImportModel[] |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/accounts/vmi/{vmiUserId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiUserId` | string | ✅ |  |

#### Request Body

**Schema:** `VmiUserModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `userId` | string | uuid |
| `role` | string |  |
| `vmiLocationIds` | string[] |  |
| `removeVmiPermissions` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiUserModel` |

##### Response Schema: `VmiUserModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `userId` | string | uuid |
| `role` | string |  |
| `vmiLocationIds` | string[] |  |
| `removeVmiPermissions` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/accounts/current/paymentprofiles

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.query` | string | ❌ |  |
| `parameter.expand` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountPaymentProfileCollectionModel` |

##### Response Schema: `AccountPaymentProfileCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `accountPaymentProfiles` | AccountPaymentProfileModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `POST` /api/v1/accounts/current/paymentprofiles

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `AccountPaymentProfileModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `description` | string |  |
| `cardType` | string |  |
| `expirationDate` | string |  |
| `maskedCardNumber` | string |  |
| `cardIdentifier` | string |  |
| `cardHolderName` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `state` | string |  |
| `postalCode` | string |  |
| `country` | string |  |
| `isDefault` | boolean |  |
| `tokenScheme` | string |  |
| `securityCode` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountPaymentProfileModel` |

##### Response Schema: `AccountPaymentProfileModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `description` | string |  |
| `cardType` | string |  |
| `expirationDate` | string |  |
| `maskedCardNumber` | string |  |
| `cardIdentifier` | string |  |
| `cardHolderName` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `state` | string |  |
| `postalCode` | string |  |
| `country` | string |  |
| `isDefault` | boolean |  |
| `tokenScheme` | string |  |
| `securityCode` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `AccountPaymentProfileId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.accountPaymentProfileId` | string (uuid) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountPaymentProfileModel` |

##### Response Schema: `AccountPaymentProfileModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `description` | string |  |
| `cardType` | string |  |
| `expirationDate` | string |  |
| `maskedCardNumber` | string |  |
| `cardIdentifier` | string |  |
| `cardHolderName` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `state` | string |  |
| `postalCode` | string |  |
| `country` | string |  |
| `isDefault` | boolean |  |
| `tokenScheme` | string |  |
| `securityCode` | string |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `AccountPaymentProfileId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.accountPaymentProfileId` | string (uuid) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountPaymentProfileModel` |

##### Response Schema: `AccountPaymentProfileModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `description` | string |  |
| `cardType` | string |  |
| `expirationDate` | string |  |
| `maskedCardNumber` | string |  |
| `cardIdentifier` | string |  |
| `cardHolderName` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `state` | string |  |
| `postalCode` | string |  |
| `country` | string |  |
| `isDefault` | boolean |  |
| `tokenScheme` | string |  |
| `securityCode` | string |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `AccountPaymentProfileId` | string | ✅ |  |

#### Request Body

**Schema:** `AccountPaymentProfileModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `description` | string |  |
| `cardType` | string |  |
| `expirationDate` | string |  |
| `maskedCardNumber` | string |  |
| `cardIdentifier` | string |  |
| `cardHolderName` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `state` | string |  |
| `postalCode` | string |  |
| `country` | string |  |
| `isDefault` | boolean |  |
| `tokenScheme` | string |  |
| `securityCode` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountPaymentProfileModel` |

##### Response Schema: `AccountPaymentProfileModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `description` | string |  |
| `cardType` | string |  |
| `expirationDate` | string |  |
| `maskedCardNumber` | string |  |
| `cardIdentifier` | string |  |
| `cardHolderName` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `state` | string |  |
| `postalCode` | string |  |
| `country` | string |  |
| `isDefault` | boolean |  |
| `tokenScheme` | string |  |
| `securityCode` | string |  |
| `properties` | object |  |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/accounts` | GET, POST |
| `/api/v1/accounts/current/paymentprofiles` | GET, POST |
| `/api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}` | GET, DELETE, PATCH |
| `/api/v1/accounts/{accountId}` | GET, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/accounts`
- `/api/v1/accounts/current/paymentprofiles`
- `/api/v1/accounts/{accountId}`

**Child / sub-resources:**

- `/api/v1/accounts/current/paymentprofiles`
- `/api/v1/accounts/vmi/import`
- `/api/v1/accounts/vmi/{vmiUserId}`
- `/api/v1/accounts/{accountId}`
- `/api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}`
- `/api/v1/accounts/{accountId}/shiptos`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{accountId}`

**Linked paths:**

- `/api/v1/accounts/{accountId}`
- `/api/v1/accounts/{accountId}/shiptos`



---

## Sessions

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/sessions/current`](#get-api-v1-sessions-current)
- [`DELETE /api/v1/sessions/current`](#delete-api-v1-sessions-current)
- [`PATCH /api/v1/sessions/current`](#patch-api-v1-sessions-current)
- [`POST /api/v1/sessions`](#post-api-v1-sessions)

---

### `GET` /api/v1/sessions/current

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `SessionModel` |

##### Response Schema: `SessionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isAuthenticated` | boolean |  |
| `hasRfqUpdates` | boolean |  |
| `userName` | string |  |
| `userProfileId` | string | uuid |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `userRolesTranslated` | string |  |
| `email` | string |  |
| `password` | string |  |
| `newPassword` | string |  |
| `resetPassword` | boolean |  |
| `activateAccount` | boolean |  |
| `resetToken` | string |  |
| `displayChangeCustomerLink` | boolean |  |
| `redirectToChangeCustomerPageOnSignIn` | boolean |  |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `language` | LanguageModel |  |
| `currency` | CurrencyModel |  |
| `deviceType` | string |  |
| `persona` | string |  |
| `personas` | PersonaModel[] |  |
| `dashboardIsHomepage` | boolean |  |
| `isSalesPerson` | boolean |  |
| `customLandingPage` | string |  |
| `hasDefaultCustomer` | boolean |  |
| `rememberMe` | boolean |  |
| `keepMeSignedIn` | boolean |  |
| `isRestrictedProductRemovedFromCart` | boolean |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `customerWasUpdated` | boolean |  |
| `isGuest` | boolean |  |
| `isRestrictedProductExistInCart` | boolean |  |
| `pickUpWarehouse` | WarehouseModel |  |
| `fulfillmentMethod` | string |  |
| `cartReminderUnsubscribeToken` | string |  |
| `cartReminderUnsubscribeEmail` | string |  |
| `displayMyAccountMenu` | boolean |  |
| `displayPricingAndInventory` | boolean |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/sessions/current

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `SessionModel` |

##### Response Schema: `SessionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isAuthenticated` | boolean |  |
| `hasRfqUpdates` | boolean |  |
| `userName` | string |  |
| `userProfileId` | string | uuid |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `userRolesTranslated` | string |  |
| `email` | string |  |
| `password` | string |  |
| `newPassword` | string |  |
| `resetPassword` | boolean |  |
| `activateAccount` | boolean |  |
| `resetToken` | string |  |
| `displayChangeCustomerLink` | boolean |  |
| `redirectToChangeCustomerPageOnSignIn` | boolean |  |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `language` | LanguageModel |  |
| `currency` | CurrencyModel |  |
| `deviceType` | string |  |
| `persona` | string |  |
| `personas` | PersonaModel[] |  |
| `dashboardIsHomepage` | boolean |  |
| `isSalesPerson` | boolean |  |
| `customLandingPage` | string |  |
| `hasDefaultCustomer` | boolean |  |
| `rememberMe` | boolean |  |
| `keepMeSignedIn` | boolean |  |
| `isRestrictedProductRemovedFromCart` | boolean |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `customerWasUpdated` | boolean |  |
| `isGuest` | boolean |  |
| `isRestrictedProductExistInCart` | boolean |  |
| `pickUpWarehouse` | WarehouseModel |  |
| `fulfillmentMethod` | string |  |
| `cartReminderUnsubscribeToken` | string |  |
| `cartReminderUnsubscribeEmail` | string |  |
| `displayMyAccountMenu` | boolean |  |
| `displayPricingAndInventory` | boolean |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/sessions/current

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `SessionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isAuthenticated` | boolean |  |
| `hasRfqUpdates` | boolean |  |
| `userName` | string |  |
| `userProfileId` | string | uuid |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `userRolesTranslated` | string |  |
| `email` | string |  |
| `password` | string |  |
| `newPassword` | string |  |
| `resetPassword` | boolean |  |
| `activateAccount` | boolean |  |
| `resetToken` | string |  |
| `displayChangeCustomerLink` | boolean |  |
| `redirectToChangeCustomerPageOnSignIn` | boolean |  |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `language` | LanguageModel |  |
| `currency` | CurrencyModel |  |
| `deviceType` | string |  |
| `persona` | string |  |
| `personas` | PersonaModel[] |  |
| `dashboardIsHomepage` | boolean |  |
| `isSalesPerson` | boolean |  |
| `customLandingPage` | string |  |
| `hasDefaultCustomer` | boolean |  |
| `rememberMe` | boolean |  |
| `keepMeSignedIn` | boolean |  |
| `isRestrictedProductRemovedFromCart` | boolean |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `customerWasUpdated` | boolean |  |
| `isGuest` | boolean |  |
| `isRestrictedProductExistInCart` | boolean |  |
| `pickUpWarehouse` | WarehouseModel |  |
| `fulfillmentMethod` | string |  |
| `cartReminderUnsubscribeToken` | string |  |
| `cartReminderUnsubscribeEmail` | string |  |
| `displayMyAccountMenu` | boolean |  |
| `displayPricingAndInventory` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `SessionModel` |

##### Response Schema: `SessionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isAuthenticated` | boolean |  |
| `hasRfqUpdates` | boolean |  |
| `userName` | string |  |
| `userProfileId` | string | uuid |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `userRolesTranslated` | string |  |
| `email` | string |  |
| `password` | string |  |
| `newPassword` | string |  |
| `resetPassword` | boolean |  |
| `activateAccount` | boolean |  |
| `resetToken` | string |  |
| `displayChangeCustomerLink` | boolean |  |
| `redirectToChangeCustomerPageOnSignIn` | boolean |  |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `language` | LanguageModel |  |
| `currency` | CurrencyModel |  |
| `deviceType` | string |  |
| `persona` | string |  |
| `personas` | PersonaModel[] |  |
| `dashboardIsHomepage` | boolean |  |
| `isSalesPerson` | boolean |  |
| `customLandingPage` | string |  |
| `hasDefaultCustomer` | boolean |  |
| `rememberMe` | boolean |  |
| `keepMeSignedIn` | boolean |  |
| `isRestrictedProductRemovedFromCart` | boolean |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `customerWasUpdated` | boolean |  |
| `isGuest` | boolean |  |
| `isRestrictedProductExistInCart` | boolean |  |
| `pickUpWarehouse` | WarehouseModel |  |
| `fulfillmentMethod` | string |  |
| `cartReminderUnsubscribeToken` | string |  |
| `cartReminderUnsubscribeEmail` | string |  |
| `displayMyAccountMenu` | boolean |  |
| `displayPricingAndInventory` | boolean |  |
| `properties` | object |  |

---

### `POST` /api/v1/sessions

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `SessionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isAuthenticated` | boolean |  |
| `hasRfqUpdates` | boolean |  |
| `userName` | string |  |
| `userProfileId` | string | uuid |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `userRolesTranslated` | string |  |
| `email` | string |  |
| `password` | string |  |
| `newPassword` | string |  |
| `resetPassword` | boolean |  |
| `activateAccount` | boolean |  |
| `resetToken` | string |  |
| `displayChangeCustomerLink` | boolean |  |
| `redirectToChangeCustomerPageOnSignIn` | boolean |  |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `language` | LanguageModel |  |
| `currency` | CurrencyModel |  |
| `deviceType` | string |  |
| `persona` | string |  |
| `personas` | PersonaModel[] |  |
| `dashboardIsHomepage` | boolean |  |
| `isSalesPerson` | boolean |  |
| `customLandingPage` | string |  |
| `hasDefaultCustomer` | boolean |  |
| `rememberMe` | boolean |  |
| `keepMeSignedIn` | boolean |  |
| `isRestrictedProductRemovedFromCart` | boolean |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `customerWasUpdated` | boolean |  |
| `isGuest` | boolean |  |
| `isRestrictedProductExistInCart` | boolean |  |
| `pickUpWarehouse` | WarehouseModel |  |
| `fulfillmentMethod` | string |  |
| `cartReminderUnsubscribeToken` | string |  |
| `cartReminderUnsubscribeEmail` | string |  |
| `displayMyAccountMenu` | boolean |  |
| `displayPricingAndInventory` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `SessionModel` |

##### Response Schema: `SessionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isAuthenticated` | boolean |  |
| `hasRfqUpdates` | boolean |  |
| `userName` | string |  |
| `userProfileId` | string | uuid |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `userRolesTranslated` | string |  |
| `email` | string |  |
| `password` | string |  |
| `newPassword` | string |  |
| `resetPassword` | boolean |  |
| `activateAccount` | boolean |  |
| `resetToken` | string |  |
| `displayChangeCustomerLink` | boolean |  |
| `redirectToChangeCustomerPageOnSignIn` | boolean |  |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `language` | LanguageModel |  |
| `currency` | CurrencyModel |  |
| `deviceType` | string |  |
| `persona` | string |  |
| `personas` | PersonaModel[] |  |
| `dashboardIsHomepage` | boolean |  |
| `isSalesPerson` | boolean |  |
| `customLandingPage` | string |  |
| `hasDefaultCustomer` | boolean |  |
| `rememberMe` | boolean |  |
| `keepMeSignedIn` | boolean |  |
| `isRestrictedProductRemovedFromCart` | boolean |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `customerWasUpdated` | boolean |  |
| `isGuest` | boolean |  |
| `isRestrictedProductExistInCart` | boolean |  |
| `pickUpWarehouse` | WarehouseModel |  |
| `fulfillmentMethod` | string |  |
| `cartReminderUnsubscribeToken` | string |  |
| `cartReminderUnsubscribeEmail` | string |  |
| `displayMyAccountMenu` | boolean |  |
| `displayPricingAndInventory` | boolean |  |
| `properties` | object |  |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/sessions/current` | GET, DELETE, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/sessions`

**Child / sub-resources:**

- `/api/v1/sessions/current`



---

## Billtos

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/billtos/{billToId}/shiptos/{shipToId}`](#get-api-v1-billtos-billtoid-shiptos-shiptoid)
- [`PATCH /api/v1/billtos/{billToId}/shiptos/{shipToId}`](#patch-api-v1-billtos-billtoid-shiptos-shiptoid)
- [`GET /api/v1/billtos/{billToId}/shiptos`](#get-api-v1-billtos-billtoid-shiptos)
- [`POST /api/v1/billtos/{billToId}/shiptos`](#post-api-v1-billtos-billtoid-shiptos)
- [`GET /api/v1/billtos`](#get-api-v1-billtos)
- [`POST /api/v1/billtos`](#post-api-v1-billtos)
- [`GET /api/v1/billtos/{billToId}`](#get-api-v1-billtos-billtoid)
- [`PATCH /api/v1/billtos/{billToId}`](#patch-api-v1-billtos-billtoid)

---

### `GET` /api/v1/billtos/{billToId}/shiptos/{shipToId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `billToId` | string | ✅ |  |
| `shipToId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ShipToModel` |

##### Response Schema: `ShipToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isNew` | boolean |  |
| `oneTimeAddress` | boolean |  |
| `label` | string |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/billtos/{billToId}/shiptos/{shipToId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `billToId` | string | ✅ |  |
| `shipToId` | string | ✅ |  |

#### Request Body

**Schema:** `ShipToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isNew` | boolean |  |
| `oneTimeAddress` | boolean |  |
| `label` | string |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ShipToModel` |

##### Response Schema: `ShipToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isNew` | boolean |  |
| `oneTimeAddress` | boolean |  |
| `label` | string |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/billtos/{billToId}/shiptos

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `billToId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `apiParameter.billToId` | string | ❌ |  |
| `apiParameter.expand` | string | ❌ |  |
| `apiParameter.filter` | string | ❌ |  |
| `apiParameter.page` | integer (int32) | ❌ |  |
| `apiParameter.pageSize` | integer (int32) | ❌ |  |
| `apiParameter.sort` | string | ❌ |  |
| `apiParameter.exclude` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ShipToCollectionModel` |

##### Response Schema: `ShipToCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `shipTos` | ShipToModel[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/billtos/{billToId}/shiptos

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `billToId` | string | ✅ |  |

#### Request Body

**Schema:** `ShipToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isNew` | boolean |  |
| `oneTimeAddress` | boolean |  |
| `label` | string |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ShipToModel` |

##### Response Schema: `ShipToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `isNew` | boolean |  |
| `oneTimeAddress` | boolean |  |
| `label` | string |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/billtos

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.expand` | string | ❌ |  |
| `parameter.filter` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.exclude` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BillToCollectionModel` |

##### Response Schema: `BillToCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `billTos` | BillToModel[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/billtos

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `BillToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `shipTosUri` | string |  |
| `isGuest` | boolean |  |
| `label` | string |  |
| `budgetEnforcementLevel` | string |  |
| `costCodeTitle` | string |  |
| `customerCurrencySymbol` | string |  |
| `costCodes` | CostCodeModel[] |  |
| `shipTos` | ShipToModel[] |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `accountsReceivable` | AccountsReceivableDto |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BillToModel` |

##### Response Schema: `BillToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `shipTosUri` | string |  |
| `isGuest` | boolean |  |
| `label` | string |  |
| `budgetEnforcementLevel` | string |  |
| `costCodeTitle` | string |  |
| `customerCurrencySymbol` | string |  |
| `costCodes` | CostCodeModel[] |  |
| `shipTos` | ShipToModel[] |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `accountsReceivable` | AccountsReceivableDto |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/billtos/{billToId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `billToId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BillToModel` |

##### Response Schema: `BillToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `shipTosUri` | string |  |
| `isGuest` | boolean |  |
| `label` | string |  |
| `budgetEnforcementLevel` | string |  |
| `costCodeTitle` | string |  |
| `customerCurrencySymbol` | string |  |
| `costCodes` | CostCodeModel[] |  |
| `shipTos` | ShipToModel[] |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `accountsReceivable` | AccountsReceivableDto |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/billtos/{billToId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `billToId` | string | ✅ |  |

#### Request Body

**Schema:** `BillToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `shipTosUri` | string |  |
| `isGuest` | boolean |  |
| `label` | string |  |
| `budgetEnforcementLevel` | string |  |
| `costCodeTitle` | string |  |
| `customerCurrencySymbol` | string |  |
| `costCodes` | CostCodeModel[] |  |
| `shipTos` | ShipToModel[] |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `accountsReceivable` | AccountsReceivableDto |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BillToModel` |

##### Response Schema: `BillToModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `shipTosUri` | string |  |
| `isGuest` | boolean |  |
| `label` | string |  |
| `budgetEnforcementLevel` | string |  |
| `costCodeTitle` | string |  |
| `customerCurrencySymbol` | string |  |
| `costCodes` | CostCodeModel[] |  |
| `shipTos` | ShipToModel[] |  |
| `validation` | CustomerValidationDto |  |
| `isDefault` | boolean |  |
| `accountsReceivable` | AccountsReceivableDto |  |
| `id` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerName` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `contactFullName` | string |  |
| `companyName` | string |  |
| `attention` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `address3` | string |  |
| `address4` | string |  |
| `city` | string |  |
| `postalCode` | string |  |
| `state` | StateModel |  |
| `country` | CountryModel |  |
| `phone` | string |  |
| `fullAddress` | string |  |
| `email` | string |  |
| `fax` | string |  |
| `isVmiLocation` | boolean |  |
| `properties` | object |  |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/billtos` | GET, POST |
| `/api/v1/billtos/{billToId}` | GET, PATCH |
| `/api/v1/billtos/{billToId}/shiptos` | GET, POST |
| `/api/v1/billtos/{billToId}/shiptos/{shipToId}` | GET, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/billtos`
- `/api/v1/billtos/{billToId}`
- `/api/v1/billtos/{billToId}/shiptos`

**Child / sub-resources:**

- `/api/v1/billtos/{billToId}`
- `/api/v1/billtos/{billToId}/shiptos`
- `/api/v1/billtos/{billToId}/shiptos/{shipToId}`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{billToId}`

**Linked paths:**

- `/api/v1/billtos/{billToId}`
- `/api/v1/billtos/{billToId}/shiptos`
- `/api/v1/billtos/{billToId}/shiptos/{shipToId}`



---

