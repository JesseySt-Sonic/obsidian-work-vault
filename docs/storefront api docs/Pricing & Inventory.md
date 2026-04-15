---
tags:
  - storefront-api
---
# Pricing & Inventory

Stateless POST-only adapters that translate storefront requests into real-time ERP lookups for prices, stock levels, and cart-level inventory validation.

---

## Contents

- [[#Realtimepricing]]
- [[#Realtimeinventory]]
- [[#Realtimecartinventory]]

---

## Realtimepricing

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`POST /api/v1/realtimepricing`](#post-api-v1-realtimepricing)

---

### `POST` /api/v1/realtimepricing

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `RealTimePricingParameter`

| Property | Type | Description |
|----------|------|-------------|
| `productPriceParameters` | ProductPriceParameter[] |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RealTimePricingModel` |

##### Response Schema: `RealTimePricingModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `realTimePricingResults` | ProductPriceDto[] |  |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Realtimeinventory

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`POST /api/v1/realtimeinventory`](#post-api-v1-realtimeinventory)

---

### `POST` /api/v1/realtimeinventory

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `RealTimeInventoryParameter`

| Property | Type | Description |
|----------|------|-------------|
| `productIds` | string[] |  |
| `properties` | object |  |
| `includeAlternateInventory` | boolean |  |
| `configurations` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RealTimeInventoryModel` |

##### Response Schema: `RealTimeInventoryModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `realTimeInventoryResults` | ProductInventoryDto[] |  |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Realtimecartinventory

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`POST /api/v1/realtimecartinventory`](#post-api-v1-realtimecartinventory)

---

### `POST` /api/v1/realtimecartinventory

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `RealTimeCartInventoryParameter`

| Property | Type | Description |
|----------|------|-------------|
| `cartId` | string | uuid |
| `warehouseIds` | string[] |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RealTimeCartInventoryModel` |

##### Response Schema: `RealTimeCartInventoryModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `warehouseAvailabilities` | object |  |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

