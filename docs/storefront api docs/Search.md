---
tags:
  - storefront-api
---
# Search

Storefront search and autocomplete. The Algolia export endpoints are read projections of catalogue data intended for background indexing jobs, not direct UI calls.

---

## Contents

- [[#Autocomplete]]
- [[#Algolia]]

---

## Autocomplete

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/autocomplete`](#get-api-v1-autocomplete)
- [`GET /api/v1/autocomplete/products`](#get-api-v1-autocomplete-products)

---

### `GET` /api/v1/autocomplete

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `autocompleteParameter.query` | string | ❌ |  |
| `autocompleteParameter.categoryEnabled` | boolean | ❌ |  |
| `autocompleteParameter.contentEnabled` | boolean | ❌ |  |
| `autocompleteParameter.productEnabled` | boolean | ❌ |  |
| `autocompleteParameter.brandEnabled` | boolean | ❌ |  |
| `autocompleteParameter.spireContent` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AutocompleteModel` |

##### Response Schema: `AutocompleteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `categories` | AutocompleteItemModel[] |  |
| `products` | ProductAutocompleteItemModel[] |  |
| `content` | AutocompleteItemModel[] |  |
| `brands` | BrandAutocompleteModel[] |  |
| `isRetailSearchCompletionResults` | boolean |  |
| `attributionToken` | string |  |
| `completionResults` | AutocompleteCompletionResultModel[] |  |
| `attributeResults` | AutocompleteAttributeResultsModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/autocomplete/products

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `model.query` | string | ❌ |  |
| `model.categoryId` | string (uuid) | ❌ |  |
| `model.maximumResults` | integer (int32) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AutocompleteProductCollectionModel` |

##### Response Schema: `AutocompleteProductCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `products` | AutocompleteProductModel[] |  |
| `properties` | object |  |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/autocomplete`

**Child / sub-resources:**

- `/api/v1/autocomplete/products`



---

## Algolia

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/algolia/export/product`](#get-api-v1-algolia-export-product)
- [`GET /api/v1/algolia/export/categorystructured`](#get-api-v1-algolia-export-categorystructured)
- [`GET /api/v1/algolia/export/category`](#get-api-v1-algolia-export-category)
- [`GET /api/v1/algolia/export/restriction`](#get-api-v1-algolia-export-restriction)

---

### `GET` /api/v1/algolia/export/product

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/algolia/export/categorystructured

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/algolia/export/category

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/algolia/export/restriction

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


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

