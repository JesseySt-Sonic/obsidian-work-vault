---
tags:
  - storefront-api
---
# VMI

Vendor-Managed Inventory — a self-contained 4-level hierarchy of locations, bins, bin counts, and notes. VMI user access is set up via the Identity & Account service.

---

## Contents

- [[#Vmilocations]]
- [[#Vmibins]]

---

## VmiLocations

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/vmiLocations/{vmiLocationId}/bins`](#get-api-v1-vmilocations-vmilocationid-bins)
- [`POST /api/v1/vmiLocations/{vmiLocationId}/bins`](#post-api-v1-vmilocations-vmilocationid-bins)
- [`DELETE /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}`](#delete-api-v1-vmilocations-vmilocationid-bins-vmibinid)
- [`PATCH /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}`](#patch-api-v1-vmilocations-vmilocationid-bins-vmibinid)
- [`POST /api/v1/vmiLocations/{vmiLocationId}/bins/batch`](#post-api-v1-vmilocations-vmilocationid-bins-batch)
- [`DELETE /api/v1/vmiLocations/{vmiLocationId}/bins/batch`](#delete-api-v1-vmilocations-vmilocationid-bins-batch)
- [`POST /api/v1/vmiLocations/{vmiLocationId}/bins/send-pdf`](#post-api-v1-vmilocations-vmilocationid-bins-send-pdf)
- [`GET /api/v1/vmiLocations`](#get-api-v1-vmilocations)
- [`POST /api/v1/vmiLocations`](#post-api-v1-vmilocations)
- [`GET /api/v1/vmiLocations/{VmiLocationId}/notes`](#get-api-v1-vmilocations-vmilocationid-notes)
- [`POST /api/v1/vmiLocations/batch`](#post-api-v1-vmilocations-batch)
- [`DELETE /api/v1/vmiLocations/batch`](#delete-api-v1-vmilocations-batch)
- [`GET /api/v1/vmiLocations/{vmiLocationId}`](#get-api-v1-vmilocations-vmilocationid)
- [`DELETE /api/v1/vmiLocations/{vmiLocationId}`](#delete-api-v1-vmilocations-vmilocationid)
- [`PATCH /api/v1/vmiLocations/{vmiLocationId}`](#patch-api-v1-vmilocations-vmilocationid)
- [`POST /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes`](#post-api-v1-vmilocations-vmilocationid-bins-vmibinid-notes)
- [`DELETE /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}`](#delete-api-v1-vmilocations-vmilocationid-bins-vmibinid-notes-vminoteid)
- [`PATCH /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}`](#patch-api-v1-vmilocations-vmilocationid-bins-vmibinid-notes-vminoteid)
- [`POST /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts`](#post-api-v1-vmilocations-vmilocationid-bins-vmibinid-bincounts)
- [`GET /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}`](#get-api-v1-vmilocations-vmilocationid-bins-vmibinid-bincounts-vmicountid)
- [`DELETE /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}`](#delete-api-v1-vmilocations-vmilocationid-bins-vmibinid-bincounts-vmicountid)
- [`PATCH /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}`](#patch-api-v1-vmilocations-vmilocationid-bins-vmibinid-bincounts-vmicountid)
- [`POST /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/batch`](#post-api-v1-vmilocations-vmilocationid-bins-vmibinid-bincounts-batch)

---

### `GET` /api/v1/vmiLocations/{vmiLocationId}/bins

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.vmiLocationId` | string (uuid) | ❌ |  |
| `parameter.filter` | string | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.searchCriteria` | string | ❌ |  |
| `parameter.binNumberFrom` | string | ❌ |  |
| `parameter.binNumberTo` | string | ❌ |  |
| `parameter.previousCountFromDate` | string (date-time) | ❌ |  |
| `parameter.previousCountToDate` | string (date-time) | ❌ |  |
| `parameter.isBelowMinimum` | boolean | ❌ |  |
| `parameter.numberOfTimesMinQtyReached` | integer (int32) | ❌ |  |
| `parameter.numberOfPreviousOrders` | integer (int32) | ❌ |  |
| `parameter.numberOfVisits` | integer (int32) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiBinCollectionModel` |

##### Response Schema: `VmiBinCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `vmiBins` | VmiBinModel[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/vmiLocations/{vmiLocationId}/bins

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |

#### Request Body

**Schema:** `VmiBinModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiLocationId` | string | uuid |
| `binNumber` | string |  |
| `productId` | string | uuid |
| `minimumQty` | number | decimal |
| `maximumQty` | number | decimal |
| `lastCountDate` | string | date-time |
| `lastCountQty` | number | decimal |
| `lastCountUserName` | string |  |
| `previousCountDate` | string | date-time |
| `previousCountQty` | number | decimal |
| `previousCountUserName` | string |  |
| `lastOrderDate` | string | date-time |
| `product` | ProductDto |  |
| `lastOrderErpOrderNumber` | string |  |
| `lastOrderWebOrderNumber` | string |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiBinModel` |

##### Response Schema: `VmiBinModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiLocationId` | string | uuid |
| `binNumber` | string |  |
| `productId` | string | uuid |
| `minimumQty` | number | decimal |
| `maximumQty` | number | decimal |
| `lastCountDate` | string | date-time |
| `lastCountQty` | number | decimal |
| `lastCountUserName` | string |  |
| `previousCountDate` | string | date-time |
| `previousCountQty` | number | decimal |
| `previousCountUserName` | string |  |
| `lastOrderDate` | string | date-time |
| `product` | ProductDto |  |
| `lastOrderErpOrderNumber` | string |  |
| `lastOrderWebOrderNumber` | string |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiBinId` | string (uuid) | ✅ |  |
| `vmiLocationId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiBinModel` |

##### Response Schema: `VmiBinModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiLocationId` | string | uuid |
| `binNumber` | string |  |
| `productId` | string | uuid |
| `minimumQty` | number | decimal |
| `maximumQty` | number | decimal |
| `lastCountDate` | string | date-time |
| `lastCountQty` | number | decimal |
| `lastCountUserName` | string |  |
| `previousCountDate` | string | date-time |
| `previousCountQty` | number | decimal |
| `previousCountUserName` | string |  |
| `lastOrderDate` | string | date-time |
| `product` | ProductDto |  |
| `lastOrderErpOrderNumber` | string |  |
| `lastOrderWebOrderNumber` | string |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |
| `vmiBinId` | string | ✅ |  |

#### Request Body

**Schema:** `VmiBinModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiLocationId` | string | uuid |
| `binNumber` | string |  |
| `productId` | string | uuid |
| `minimumQty` | number | decimal |
| `maximumQty` | number | decimal |
| `lastCountDate` | string | date-time |
| `lastCountQty` | number | decimal |
| `lastCountUserName` | string |  |
| `previousCountDate` | string | date-time |
| `previousCountQty` | number | decimal |
| `previousCountUserName` | string |  |
| `lastOrderDate` | string | date-time |
| `product` | ProductDto |  |
| `lastOrderErpOrderNumber` | string |  |
| `lastOrderWebOrderNumber` | string |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiBinModel` |

##### Response Schema: `VmiBinModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiLocationId` | string | uuid |
| `binNumber` | string |  |
| `productId` | string | uuid |
| `minimumQty` | number | decimal |
| `maximumQty` | number | decimal |
| `lastCountDate` | string | date-time |
| `lastCountQty` | number | decimal |
| `lastCountUserName` | string |  |
| `previousCountDate` | string | date-time |
| `previousCountQty` | number | decimal |
| `previousCountUserName` | string |  |
| `lastOrderDate` | string | date-time |
| `product` | ProductDto |  |
| `lastOrderErpOrderNumber` | string |  |
| `lastOrderWebOrderNumber` | string |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `properties` | object |  |

---

### `POST` /api/v1/vmiLocations/{vmiLocationId}/bins/batch

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `VmiBinModel[]`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiLocationId` | string | uuid |
| `binNumber` | string |  |
| `productId` | string | uuid |
| `minimumQty` | number | decimal |
| `maximumQty` | number | decimal |
| `lastCountDate` | string | date-time |
| `lastCountQty` | number | decimal |
| `lastCountUserName` | string |  |
| `previousCountDate` | string | date-time |
| `previousCountQty` | number | decimal |
| `previousCountUserName` | string |  |
| `lastOrderDate` | string | date-time |
| `product` | ProductDto |  |
| `lastOrderErpOrderNumber` | string |  |
| `lastOrderWebOrderNumber` | string |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiBinCollectionModel` |

##### Response Schema: `VmiBinCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `vmiBins` | VmiBinModel[] |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/vmiLocations/{vmiLocationId}/bins/batch

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `ids` | string[] | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiBinCollectionModel` |

##### Response Schema: `VmiBinCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `vmiBins` | VmiBinModel[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/vmiLocations/{vmiLocationId}/bins/send-pdf

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `VmiBinPdfParameter`

| Property | Type | Description |
|----------|------|-------------|
| `lineIds` | string[] |  |
| `layout` | string |  |
| `barcodeFormat` | string |  |
| `barcodeField` | string |  |
| `displayFields` | string[] |  |
| `addOverlay` | boolean |  |
| `vmiBinDetailsPageUrl` | string |  |
| `vmiLocationId` | string | uuid |
| `filter` | string |  |
| `sort` | string |  |
| `page` | integer | int32 |
| `pageSize` | integer | int32 |
| `searchCriteria` | string |  |
| `binNumberFrom` | string |  |
| `binNumberTo` | string |  |
| `previousCountFromDate` | string | date-time |
| `previousCountToDate` | string | date-time |
| `isBelowMinimum` | boolean |  |
| `numberOfTimesMinQtyReached` | integer | int32 |
| `numberOfPreviousOrders` | integer | int32 |
| `numberOfVisits` | integer | int32 |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiBinCollectionModel` |

##### Response Schema: `VmiBinCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `vmiBins` | VmiBinModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/vmiLocations

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.userId` | string (uuid) | ❌ |  |
| `parameter.filter` | string | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiLocationCollectionModel` |

##### Response Schema: `VmiLocationCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `vmiLocations` | VmiLocationModel[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/vmiLocations

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `VmiLocationModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `billToId` | string | uuid |
| `useBins` | boolean |  |
| `isPrimaryLocation` | boolean |  |
| `shipToId` | string | uuid |
| `customer` | BaseAddressModel |  |
| `customerLabel` | string |  |
| `note` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiLocationModel` |

##### Response Schema: `VmiLocationModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `billToId` | string | uuid |
| `useBins` | boolean |  |
| `isPrimaryLocation` | boolean |  |
| `shipToId` | string | uuid |
| `customer` | BaseAddressModel |  |
| `customerLabel` | string |  |
| `note` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/vmiLocations/{VmiLocationId}/notes

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `VmiLocationId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.vmiLocationId` | string (uuid) | ❌ |  |
| `parameter.vmiBinId` | string (uuid) | ❌ |  |
| `parameter.vmiNoteId` | string (uuid) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiNoteCollectionModel` |

##### Response Schema: `VmiNoteCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `vmiNotes` | VmiNoteModel[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/vmiLocations/batch

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `VmiLocationBatchCollectionParameter`

| Property | Type | Description |
|----------|------|-------------|
| `vmiLocations` | VmiLocationModel[] |  |
| `validationOnly` | boolean |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiLocationCollectionModel` |

##### Response Schema: `VmiLocationCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `vmiLocations` | VmiLocationModel[] |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/vmiLocations/batch

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `ids` | string[] | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiLocationCollectionModel` |

##### Response Schema: `VmiLocationCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `vmiLocations` | VmiLocationModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/vmiLocations/{vmiLocationId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.vmiLocationId` | string (uuid) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiLocationModel` |

##### Response Schema: `VmiLocationModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `billToId` | string | uuid |
| `useBins` | boolean |  |
| `isPrimaryLocation` | boolean |  |
| `shipToId` | string | uuid |
| `customer` | BaseAddressModel |  |
| `customerLabel` | string |  |
| `note` | string |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/vmiLocations/{vmiLocationId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string (uuid) | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiLocationModel` |

##### Response Schema: `VmiLocationModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `billToId` | string | uuid |
| `useBins` | boolean |  |
| `isPrimaryLocation` | boolean |  |
| `shipToId` | string | uuid |
| `customer` | BaseAddressModel |  |
| `customerLabel` | string |  |
| `note` | string |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/vmiLocations/{vmiLocationId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |

#### Request Body

**Schema:** `VmiLocationModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `billToId` | string | uuid |
| `useBins` | boolean |  |
| `isPrimaryLocation` | boolean |  |
| `shipToId` | string | uuid |
| `customer` | BaseAddressModel |  |
| `customerLabel` | string |  |
| `note` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiLocationModel` |

##### Response Schema: `VmiLocationModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `billToId` | string | uuid |
| `useBins` | boolean |  |
| `isPrimaryLocation` | boolean |  |
| `shipToId` | string | uuid |
| `customer` | BaseAddressModel |  |
| `customerLabel` | string |  |
| `note` | string |  |
| `properties` | object |  |

---

### `POST` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |
| `vmiBinId` | string | ✅ |  |

#### Request Body

**Schema:** `VmiNoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `note` | string |  |
| `includeOnOrder` | boolean |  |
| `createdOn` | string | date-time |
| `vmiBinProductId` | string | uuid |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiNoteModel` |

##### Response Schema: `VmiNoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `note` | string |  |
| `includeOnOrder` | boolean |  |
| `createdOn` | string | date-time |
| `vmiBinProductId` | string | uuid |
| `properties` | object |  |

---

### `DELETE` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiNoteId` | string (uuid) | ✅ |  |
| `vmiLocationId` | string | ✅ |  |
| `vmiBinId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiNoteModel` |

##### Response Schema: `VmiNoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `note` | string |  |
| `includeOnOrder` | boolean |  |
| `createdOn` | string | date-time |
| `vmiBinProductId` | string | uuid |
| `properties` | object |  |

---

### `PATCH` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |
| `vmiBinId` | string | ✅ |  |
| `vmiNoteId` | string | ✅ |  |

#### Request Body

**Schema:** `VmiNoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `note` | string |  |
| `includeOnOrder` | boolean |  |
| `createdOn` | string | date-time |
| `vmiBinProductId` | string | uuid |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiNoteModel` |

##### Response Schema: `VmiNoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `note` | string |  |
| `includeOnOrder` | boolean |  |
| `createdOn` | string | date-time |
| `vmiBinProductId` | string | uuid |
| `properties` | object |  |

---

### `POST` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |
| `vmiBinId` | string | ✅ |  |

#### Request Body

**Schema:** `VmiCountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `productId` | string | uuid |
| `count` | number | decimal |
| `createdOn` | string | date-time |
| `createdBy` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiCountModel` |

##### Response Schema: `VmiCountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `productId` | string | uuid |
| `count` | number | decimal |
| `createdOn` | string | date-time |
| `createdBy` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |
| `vmiBinId` | string | ✅ |  |
| `vmiCountId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.vmiLocationId` | string (uuid) | ❌ |  |
| `parameter.vmiBinId` | string (uuid) | ❌ |  |
| `parameter.vmiCountId` | string (uuid) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiCountModel` |

##### Response Schema: `VmiCountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `productId` | string | uuid |
| `count` | number | decimal |
| `createdOn` | string | date-time |
| `createdBy` | string |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiCountId` | string (uuid) | ✅ |  |
| `vmiLocationId` | string | ✅ |  |
| `vmiBinId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiCountModel` |

##### Response Schema: `VmiCountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `productId` | string | uuid |
| `count` | number | decimal |
| `createdOn` | string | date-time |
| `createdBy` | string |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |
| `vmiBinId` | string | ✅ |  |
| `vmiCountId` | string | ✅ |  |

#### Request Body

**Schema:** `VmiCountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `productId` | string | uuid |
| `count` | number | decimal |
| `createdOn` | string | date-time |
| `createdBy` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiCountModel` |

##### Response Schema: `VmiCountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `productId` | string | uuid |
| `count` | number | decimal |
| `createdOn` | string | date-time |
| `createdBy` | string |  |
| `properties` | object |  |

---

### `POST` /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/batch

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `vmiLocationId` | string | ✅ |  |
| `vmiBinId` | string | ✅ |  |

#### Request Body

**Schema:** `VmiCountModel[]`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `productId` | string | uuid |
| `count` | number | decimal |
| `createdOn` | string | date-time |
| `createdBy` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiCountModel` |

##### Response Schema: `VmiCountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `vmiBinId` | string | uuid |
| `productId` | string | uuid |
| `count` | number | decimal |
| `createdOn` | string | date-time |
| `createdBy` | string |  |
| `properties` | object |  |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/vmiLocations` | GET, POST |
| `/api/v1/vmiLocations/batch` | POST, DELETE |
| `/api/v1/vmiLocations/{vmiLocationId}` | GET, DELETE, PATCH |
| `/api/v1/vmiLocations/{vmiLocationId}/bins` | GET, POST |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/batch` | POST, DELETE |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}` | DELETE, PATCH |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}` | GET, DELETE, PATCH |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}` | DELETE, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/vmiLocations`
- `/api/v1/vmiLocations/{vmiLocationId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes`

**Child / sub-resources:**

- `/api/v1/vmiLocations/batch`
- `/api/v1/vmiLocations/{VmiLocationId}/notes`
- `/api/v1/vmiLocations/{vmiLocationId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/batch`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/send-pdf`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/batch`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{vmiLocationId}`

**Linked paths:**

- `/api/v1/vmiLocations/{vmiLocationId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/batch`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/send-pdf`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/batch`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}`

##### `{vmiBinId}`

**Linked paths:**

- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/batch`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes`
- `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}`



---

## VmiBins

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/vmiBins/count`](#get-api-v1-vmibins-count)

---

### `GET` /api/v1/vmiBins/count

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.isBelowMinimum` | boolean | ❌ |  |
| `parameter.numberOfTimesMinQtyReached` | integer (int32) | ❌ |  |
| `parameter.numberOfPreviousOrders` | integer (int32) | ❌ |  |
| `parameter.numberOfVisits` | integer (int32) | ❌ |  |
| `parameter.vmiLocationId` | string (uuid) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `VmiBinCountModel` |

##### Response Schema: `VmiBinCountModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `count` | integer | int32 |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

