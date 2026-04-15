---
tags:
  - storefront-api
---
# Order

Order history, submission, returns, approvals, quotes, job quotes, and invoices. Follows the cart → approval → order lifecycle with `{cartId}` as the shared key into Commerce.

---

## Contents

- [[#Orders]]
- [[#Orderapprovals]]
- [[#Quotes]]
- [[#Jobquotes]]
- [[#Invoices]]
- [[#Orderfeed]]
- [[#Orderstatusmappings]]

---

## Orders

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/orders`](#get-api-v1-orders)
- [`GET /api/v1/orders/{orderId}`](#get-api-v1-orders-orderid)
- [`PATCH /api/v1/orders/{orderId}`](#patch-api-v1-orders-orderid)
- [`POST /api/v1/orders/{orderId}/returns`](#post-api-v1-orders-orderid-returns)
- [`POST /api/v1/orders/shareorder`](#post-api-v1-orders-shareorder)

---

### `GET` /api/v1/orders

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.orderNumber` | string | ❌ |  |
| `parameter.poNumber` | string | ❌ |  |
| `parameter.search` | string | ❌ |  |
| `parameter.status` | string[] | ❌ |  |
| `parameter.customerSequence` | string | ❌ |  |
| `parameter.fromDate` | string (date-time) | ❌ |  |
| `parameter.toDate` | string (date-time) | ❌ |  |
| `parameter.orderTotalOperator` | string | ❌ |  |
| `parameter.orderTotal` | number (decimal) | ❌ |  |
| `parameter.productErpNumber` | string | ❌ |  |
| `parameter.currentPage` | integer (int32) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.vmiOrdersOnly` | boolean | ❌ |  |
| `parameter.vmiLocationId` | string (uuid) | ❌ |  |
| `parameter.vmiBinId` | string (uuid) | ❌ |  |
| `parameter.showMyOrders` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `OrderCollectionModel` |

##### Response Schema: `OrderCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `orders` | OrderModel[] |  |
| `pagination` | PaginationModel |  |
| `showErpOrderNumber` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/orders/{orderId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `orderId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `OrderModel` |

##### Response Schema: `OrderModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `erpOrderNumber` | string |  |
| `webOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `status` | string |  |
| `statusDisplay` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerPO` | string |  |
| `currencyCode` | string |  |
| `currencySymbol` | string |  |
| `terms` | string |  |
| `shipCode` | string |  |
| `salesperson` | string |  |
| `btCompanyName` | string |  |
| `btAddress1` | string |  |
| `btAddress2` | string |  |
| `btAddress3` | string |  |
| `btAddress4` | string |  |
| `billToCity` | string |  |
| `billToState` | string |  |
| `billToPostalCode` | string |  |
| `btCountry` | string |  |
| `stCompanyName` | string |  |
| `stAddress1` | string |  |
| `stAddress2` | string |  |
| `stAddress3` | string |  |
| `stAddress4` | string |  |
| `shipToCity` | string |  |
| `shipToState` | string |  |
| `shipToPostalCode` | string |  |
| `stCountry` | string |  |
| `notes` | string |  |
| `productTotal` | number | decimal |
| `orderSubTotal` | number | decimal |
| `discountAmount` | number | decimal |
| `orderDiscountAmount` | number | decimal |
| `productDiscountAmount` | number | decimal |
| `shippingAndHandling` | number | decimal |
| `shippingCharges` | number | decimal |
| `handlingCharges` | number | decimal |
| `otherCharges` | number | decimal |
| `taxAmount` | number | decimal |
| `orderTotal` | number | decimal |
| `modifyDate` | string | date-time |
| `requestedDeliveryDateDisplay` | string | date-time |
| `orderLines` | OrderLineModel[] |  |
| `orderPromotions` | OrderPromotionModel[] |  |
| `shipmentPackages` | ShipmentPackageDto[] |  |
| `returnReasons` | string[] |  |
| `orderHistoryTaxes` | OrderHistoryTaxDto[] |  |
| `productTotalDisplay` | string |  |
| `orderSubTotalDisplay` | string |  |
| `orderTotalDisplay` | string |  |
| `orderGrandTotalDisplay` | string |  |
| `discountAmountDisplay` | string |  |
| `orderDiscountAmountDisplay` | string |  |
| `productDiscountAmountDisplay` | string |  |
| `taxAmountDisplay` | string |  |
| `totalTaxDisplay` | string |  |
| `shippingAndHandlingDisplay` | string |  |
| `shippingChargesDisplay` | string |  |
| `handlingChargesDisplay` | string |  |
| `otherChargesDisplay` | string |  |
| `canAddToCart` | boolean |  |
| `canAddAllToCart` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `shipViaDescription` | string |  |
| `fulfillmentMethod` | string |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string |  |
| `vmiLocationName` | string |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/orders/{orderId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `orderId` | string | ✅ |  |

#### Request Body

**Schema:** `OrderModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `erpOrderNumber` | string |  |
| `webOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `status` | string |  |
| `statusDisplay` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerPO` | string |  |
| `currencyCode` | string |  |
| `currencySymbol` | string |  |
| `terms` | string |  |
| `shipCode` | string |  |
| `salesperson` | string |  |
| `btCompanyName` | string |  |
| `btAddress1` | string |  |
| `btAddress2` | string |  |
| `btAddress3` | string |  |
| `btAddress4` | string |  |
| `billToCity` | string |  |
| `billToState` | string |  |
| `billToPostalCode` | string |  |
| `btCountry` | string |  |
| `stCompanyName` | string |  |
| `stAddress1` | string |  |
| `stAddress2` | string |  |
| `stAddress3` | string |  |
| `stAddress4` | string |  |
| `shipToCity` | string |  |
| `shipToState` | string |  |
| `shipToPostalCode` | string |  |
| `stCountry` | string |  |
| `notes` | string |  |
| `productTotal` | number | decimal |
| `orderSubTotal` | number | decimal |
| `discountAmount` | number | decimal |
| `orderDiscountAmount` | number | decimal |
| `productDiscountAmount` | number | decimal |
| `shippingAndHandling` | number | decimal |
| `shippingCharges` | number | decimal |
| `handlingCharges` | number | decimal |
| `otherCharges` | number | decimal |
| `taxAmount` | number | decimal |
| `orderTotal` | number | decimal |
| `modifyDate` | string | date-time |
| `requestedDeliveryDateDisplay` | string | date-time |
| `orderLines` | OrderLineModel[] |  |
| `orderPromotions` | OrderPromotionModel[] |  |
| `shipmentPackages` | ShipmentPackageDto[] |  |
| `returnReasons` | string[] |  |
| `orderHistoryTaxes` | OrderHistoryTaxDto[] |  |
| `productTotalDisplay` | string |  |
| `orderSubTotalDisplay` | string |  |
| `orderTotalDisplay` | string |  |
| `orderGrandTotalDisplay` | string |  |
| `discountAmountDisplay` | string |  |
| `orderDiscountAmountDisplay` | string |  |
| `productDiscountAmountDisplay` | string |  |
| `taxAmountDisplay` | string |  |
| `totalTaxDisplay` | string |  |
| `shippingAndHandlingDisplay` | string |  |
| `shippingChargesDisplay` | string |  |
| `handlingChargesDisplay` | string |  |
| `otherChargesDisplay` | string |  |
| `canAddToCart` | boolean |  |
| `canAddAllToCart` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `shipViaDescription` | string |  |
| `fulfillmentMethod` | string |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string |  |
| `vmiLocationName` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `OrderModel` |

##### Response Schema: `OrderModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `erpOrderNumber` | string |  |
| `webOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `status` | string |  |
| `statusDisplay` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerPO` | string |  |
| `currencyCode` | string |  |
| `currencySymbol` | string |  |
| `terms` | string |  |
| `shipCode` | string |  |
| `salesperson` | string |  |
| `btCompanyName` | string |  |
| `btAddress1` | string |  |
| `btAddress2` | string |  |
| `btAddress3` | string |  |
| `btAddress4` | string |  |
| `billToCity` | string |  |
| `billToState` | string |  |
| `billToPostalCode` | string |  |
| `btCountry` | string |  |
| `stCompanyName` | string |  |
| `stAddress1` | string |  |
| `stAddress2` | string |  |
| `stAddress3` | string |  |
| `stAddress4` | string |  |
| `shipToCity` | string |  |
| `shipToState` | string |  |
| `shipToPostalCode` | string |  |
| `stCountry` | string |  |
| `notes` | string |  |
| `productTotal` | number | decimal |
| `orderSubTotal` | number | decimal |
| `discountAmount` | number | decimal |
| `orderDiscountAmount` | number | decimal |
| `productDiscountAmount` | number | decimal |
| `shippingAndHandling` | number | decimal |
| `shippingCharges` | number | decimal |
| `handlingCharges` | number | decimal |
| `otherCharges` | number | decimal |
| `taxAmount` | number | decimal |
| `orderTotal` | number | decimal |
| `modifyDate` | string | date-time |
| `requestedDeliveryDateDisplay` | string | date-time |
| `orderLines` | OrderLineModel[] |  |
| `orderPromotions` | OrderPromotionModel[] |  |
| `shipmentPackages` | ShipmentPackageDto[] |  |
| `returnReasons` | string[] |  |
| `orderHistoryTaxes` | OrderHistoryTaxDto[] |  |
| `productTotalDisplay` | string |  |
| `orderSubTotalDisplay` | string |  |
| `orderTotalDisplay` | string |  |
| `orderGrandTotalDisplay` | string |  |
| `discountAmountDisplay` | string |  |
| `orderDiscountAmountDisplay` | string |  |
| `productDiscountAmountDisplay` | string |  |
| `taxAmountDisplay` | string |  |
| `totalTaxDisplay` | string |  |
| `shippingAndHandlingDisplay` | string |  |
| `shippingChargesDisplay` | string |  |
| `handlingChargesDisplay` | string |  |
| `otherChargesDisplay` | string |  |
| `canAddToCart` | boolean |  |
| `canAddAllToCart` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `shipViaDescription` | string |  |
| `fulfillmentMethod` | string |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string |  |
| `vmiLocationName` | string |  |
| `properties` | object |  |

---

### `POST` /api/v1/orders/{orderId}/returns

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `orderId` | string | ✅ |  |

#### Request Body

**Schema:** `RmaModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `orderNumber` | string |  |
| `notes` | string |  |
| `message` | string |  |
| `rmaLines` | RmaLineDto[] |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RmaModel` |

##### Response Schema: `RmaModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `orderNumber` | string |  |
| `notes` | string |  |
| `message` | string |  |
| `rmaLines` | RmaLineDto[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/orders/shareorder

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `ShareOrderModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `stEmail` | string |  |
| `stPostalCode` | string |  |
| `emailTo` | string |  |
| `emailFrom` | string |  |
| `subject` | string |  |
| `message` | string |  |
| `entityId` | string |  |
| `entityName` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ShareEntityModel` |

##### Response Schema: `ShareEntityModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `emailTo` | string |  |
| `emailFrom` | string |  |
| `subject` | string |  |
| `message` | string |  |
| `entityId` | string |  |
| `entityName` | string |  |
| `properties` | object |  |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/orders/{orderId}` | GET, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/orders`
- `/api/v1/orders/{orderId}`

**Child / sub-resources:**

- `/api/v1/orders/shareorder`
- `/api/v1/orders/{orderId}`
- `/api/v1/orders/{orderId}/returns`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{orderId}`

**Linked paths:**

- `/api/v1/orders/{orderId}`
- `/api/v1/orders/{orderId}/returns`

#### Shared Models

These response/request models are also used by other API sections:

| Model | Also used in |
|-------|--------------|
| `ShareEntityModel` | Invoices |



---

## Orderapprovals

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/orderapprovals`](#get-api-v1-orderapprovals)
- [`GET /api/v1/orderapprovals/{cartId}`](#get-api-v1-orderapprovals-cartid)

---

### `GET` /api/v1/orderapprovals

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.shipToId` | string (uuid) | ❌ |  |
| `parameter.orderNumber` | string | ❌ |  |
| `parameter.fromDate` | string (date-time) | ❌ |  |
| `parameter.toDate` | string (date-time) | ❌ |  |
| `parameter.orderTotalOperator` | string | ❌ |  |
| `parameter.orderTotal` | number (decimal) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `OrderApprovalCollectionModel` |

##### Response Schema: `OrderApprovalCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `cartCollection` | CartModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/orderapprovals/{cartId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CartModel` |

##### Response Schema: `CartModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `cartLinesUri` | string |  |
| `id` | string |  |
| `trackId` | string |  |
| `status` | string |  |
| `statusDisplay` | string |  |
| `type` | string |  |
| `typeDisplay` | string |  |
| `orderNumber` | string |  |
| `erpOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `shipToLabel` | string |  |
| `notes` | string |  |
| `carrier` | CarrierDto |  |
| `shipVia` | ShipViaDto |  |
| `paymentMethod` | PaymentMethodDto |  |
| `fulfillmentMethod` | string |  |
| `requestedPickupDate` | string |  |
| `poNumber` | string |  |
| `promotionCode` | string |  |
| `initiatedByUserName` | string |  |
| `totalQtyOrdered` | integer | int32 |
| `lineCount` | integer | int32 |
| `totalCountDisplay` | integer | int32 |
| `quoteRequiredCount` | integer | int32 |
| `orderSubTotal` | number | decimal |
| `orderSubTotalDisplay` | string |  |
| `orderSubTotalWithOutProductDiscounts` | number | decimal |
| `orderSubTotalWithOutProductDiscountsDisplay` | string |  |
| `totalTax` | number | decimal |
| `totalTaxDisplay` | string |  |
| `shippingAndHandling` | number | decimal |
| `shippingAndHandlingDisplay` | string |  |
| `orderGrandTotal` | number | decimal |
| `orderGrandTotalDisplay` | string |  |
| `costCodeLabel` | string |  |
| `isAuthenticated` | boolean |  |
| `isGuestOrder` | boolean |  |
| `isSalesperson` | boolean |  |
| `isSubscribed` | boolean |  |
| `requiresPoNumber` | boolean |  |
| `displayContinueShoppingLink` | boolean |  |
| `canModifyOrder` | boolean |  |
| `canSaveOrder` | boolean |  |
| `canBypassCheckoutAddress` | boolean |  |
| `canRequisition` | boolean |  |
| `canRequestQuote` | boolean |  |
| `canEditCostCode` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `showLineNotes` | boolean |  |
| `showCostCode` | boolean |  |
| `showNewsletterSignup` | boolean |  |
| `showPoNumber` | boolean |  |
| `showCreditCard` | boolean |  |
| `showECheck` | boolean |  |
| `showPayPal` | boolean |  |
| `isAwaitingApproval` | boolean |  |
| `requiresApproval` | boolean |  |
| `approverReason` | string |  |
| `hasApprover` | boolean |  |
| `salespersonName` | string |  |
| `paymentOptions` | PaymentOptionsDto |  |
| `costCodes` | CostCodeDto[] |  |
| `carriers` | CarrierDto[] |  |
| `warehouses` | WarehouseDto[] |  |
| `cartLines` | CartLineModel[] |  |
| `customerOrderTaxes` | CustomerOrderTaxDto[] |  |
| `canCheckOut` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `currencySymbol` | string |  |
| `requestedDeliveryDate` | string |  |
| `requestedDeliveryDateDisplay` | string | date-time |
| `cartNotPriced` | boolean |  |
| `messages` | string[] |  |
| `creditCardBillingAddress` | CreditCardBillingAddressDto |  |
| `alsoPurchasedProducts` | ProductDto[] |  |
| `requestedPickupDateDisplay` | string | date-time |
| `taxFailureReason` | string |  |
| `failedToGetRealTimeInventory` | boolean |  |
| `unassignCart` | boolean |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string | uuid |
| `additionalEmails` | string |  |
| `defaultWarehouse` | WarehouseModel |  |
| `properties` | object |  |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/orderapprovals`

**Child / sub-resources:**

- `/api/v1/orderapprovals/{cartId}`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{cartId}`

**Also used in tags:** Carts  
**Linked paths:**

- `/api/v1/carts/{cartId}`
- `/api/v1/carts/{cartId}/cartlines`
- `/api/v1/carts/{cartId}/cartlines/batch`
- `/api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}`
- `/api/v1/carts/{cartId}/cartlines/{cartLineId}`
- `/api/v1/carts/{cartId}/promotions`
- `/api/v1/carts/{cartId}/promotions/{promotionId}`
- `/api/v1/orderapprovals/{cartId}`

#### Shared Models

These response/request models are also used by other API sections:

| Model | Also used in |
|-------|--------------|
| `CartModel` | Carts |



---

## Quotes

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/quotes`](#get-api-v1-quotes)
- [`POST /api/v1/quotes`](#post-api-v1-quotes)
- [`GET /api/v1/quotes/{quoteId}`](#get-api-v1-quotes-quoteid)
- [`DELETE /api/v1/quotes/{quoteId}`](#delete-api-v1-quotes-quoteid)
- [`PATCH /api/v1/quotes/{quoteId}`](#patch-api-v1-quotes-quoteid)
- [`POST /api/v1/quotes/{quoteId}/messages`](#post-api-v1-quotes-quoteid-messages)
- [`GET /api/v1/quotes/{quoteId}/quotelines/{quoteLineId}`](#get-api-v1-quotes-quoteid-quotelines-quotelineid)
- [`PATCH /api/v1/quotes/{quoteId}/quotelines/{quoteLineId}`](#patch-api-v1-quotes-quoteid-quotelines-quotelineid)

---

### `GET` /api/v1/quotes

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `quoteParameter.userId` | string (uuid) | ❌ |  |
| `quoteParameter.salesRepNumber` | string | ❌ |  |
| `quoteParameter.customerId` | string (uuid) | ❌ |  |
| `quoteParameter.statuses` | string[] | ❌ |  |
| `quoteParameter.quoteNumber` | string | ❌ |  |
| `quoteParameter.fromDate` | string (date-time) | ❌ |  |
| `quoteParameter.toDate` | string (date-time) | ❌ |  |
| `quoteParameter.expireFromDate` | string (date-time) | ❌ |  |
| `quoteParameter.expireToDate` | string (date-time) | ❌ |  |
| `quoteParameter.startPage` | integer (int32) | ❌ |  |
| `quoteParameter.page` | integer (int32) | ❌ |  |
| `quoteParameter.pageSize` | integer (int32) | ❌ |  |
| `quoteParameter.types` | string[] | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `QuoteCollectionModel` |

##### Response Schema: `QuoteCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `quotes` | QuoteModel[] |  |
| `pagination` | PaginationModel |  |
| `salespersonList` | SalespersonModel[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/quotes

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `QuoteParameter`

| Property | Type | Description |
|----------|------|-------------|
| `quoteId` | string |  |
| `status` | string |  |
| `note` | string |  |
| `userId` | string | uuid |
| `expirationDate` | string | date-time |
| `calculationMethod` | integer | int32 |
| `percent` | number | double |
| `isJobQuote` | boolean |  |
| `jobName` | string |  |
| `orderQuantities` | QuoteLineModel[] |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `QuoteModel` |

##### Response Schema: `QuoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `quoteLinesUri` | string |  |
| `quoteNumber` | string |  |
| `expirationDate` | string | date-time |
| `customerNumber` | string |  |
| `customerName` | string |  |
| `shipToFullAddress` | string |  |
| `quoteLineCollection` | QuoteLineModel[] |  |
| `userName` | string |  |
| `isEditable` | boolean |  |
| `messageCollection` | MessageModel[] |  |
| `calculationMethods` | CalculationMethod[] |  |
| `isJobQuote` | boolean |  |
| `jobName` | string |  |
| `cartLinesUri` | string |  |
| `id` | string |  |
| `trackId` | string |  |
| `status` | string |  |
| `statusDisplay` | string |  |
| `type` | string |  |
| `typeDisplay` | string |  |
| `orderNumber` | string |  |
| `erpOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `shipToLabel` | string |  |
| `notes` | string |  |
| `carrier` | CarrierDto |  |
| `shipVia` | ShipViaDto |  |
| `paymentMethod` | PaymentMethodDto |  |
| `fulfillmentMethod` | string |  |
| `requestedPickupDate` | string |  |
| `poNumber` | string |  |
| `promotionCode` | string |  |
| `initiatedByUserName` | string |  |
| `totalQtyOrdered` | integer | int32 |
| `lineCount` | integer | int32 |
| `totalCountDisplay` | integer | int32 |
| `quoteRequiredCount` | integer | int32 |
| `orderSubTotal` | number | decimal |
| `orderSubTotalDisplay` | string |  |
| `orderSubTotalWithOutProductDiscounts` | number | decimal |
| `orderSubTotalWithOutProductDiscountsDisplay` | string |  |
| `totalTax` | number | decimal |
| `totalTaxDisplay` | string |  |
| `shippingAndHandling` | number | decimal |
| `shippingAndHandlingDisplay` | string |  |
| `orderGrandTotal` | number | decimal |
| `orderGrandTotalDisplay` | string |  |
| `costCodeLabel` | string |  |
| `isAuthenticated` | boolean |  |
| `isGuestOrder` | boolean |  |
| `isSalesperson` | boolean |  |
| `isSubscribed` | boolean |  |
| `requiresPoNumber` | boolean |  |
| `displayContinueShoppingLink` | boolean |  |
| `canModifyOrder` | boolean |  |
| `canSaveOrder` | boolean |  |
| `canBypassCheckoutAddress` | boolean |  |
| `canRequisition` | boolean |  |
| `canRequestQuote` | boolean |  |
| `canEditCostCode` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `showLineNotes` | boolean |  |
| `showCostCode` | boolean |  |
| `showNewsletterSignup` | boolean |  |
| `showPoNumber` | boolean |  |
| `showCreditCard` | boolean |  |
| `showECheck` | boolean |  |
| `showPayPal` | boolean |  |
| `isAwaitingApproval` | boolean |  |
| `requiresApproval` | boolean |  |
| `approverReason` | string |  |
| `hasApprover` | boolean |  |
| `salespersonName` | string |  |
| `paymentOptions` | PaymentOptionsDto |  |
| `costCodes` | CostCodeDto[] |  |
| `carriers` | CarrierDto[] |  |
| `warehouses` | WarehouseDto[] |  |
| `cartLines` | CartLineModel[] |  |
| `customerOrderTaxes` | CustomerOrderTaxDto[] |  |
| `canCheckOut` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `currencySymbol` | string |  |
| `requestedDeliveryDate` | string |  |
| `requestedDeliveryDateDisplay` | string | date-time |
| `cartNotPriced` | boolean |  |
| `messages` | string[] |  |
| `creditCardBillingAddress` | CreditCardBillingAddressDto |  |
| `alsoPurchasedProducts` | ProductDto[] |  |
| `requestedPickupDateDisplay` | string | date-time |
| `taxFailureReason` | string |  |
| `failedToGetRealTimeInventory` | boolean |  |
| `unassignCart` | boolean |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string | uuid |
| `additionalEmails` | string |  |
| `defaultWarehouse` | WarehouseModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/quotes/{quoteId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `quoteId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `QuoteModel` |

##### Response Schema: `QuoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `quoteLinesUri` | string |  |
| `quoteNumber` | string |  |
| `expirationDate` | string | date-time |
| `customerNumber` | string |  |
| `customerName` | string |  |
| `shipToFullAddress` | string |  |
| `quoteLineCollection` | QuoteLineModel[] |  |
| `userName` | string |  |
| `isEditable` | boolean |  |
| `messageCollection` | MessageModel[] |  |
| `calculationMethods` | CalculationMethod[] |  |
| `isJobQuote` | boolean |  |
| `jobName` | string |  |
| `cartLinesUri` | string |  |
| `id` | string |  |
| `trackId` | string |  |
| `status` | string |  |
| `statusDisplay` | string |  |
| `type` | string |  |
| `typeDisplay` | string |  |
| `orderNumber` | string |  |
| `erpOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `shipToLabel` | string |  |
| `notes` | string |  |
| `carrier` | CarrierDto |  |
| `shipVia` | ShipViaDto |  |
| `paymentMethod` | PaymentMethodDto |  |
| `fulfillmentMethod` | string |  |
| `requestedPickupDate` | string |  |
| `poNumber` | string |  |
| `promotionCode` | string |  |
| `initiatedByUserName` | string |  |
| `totalQtyOrdered` | integer | int32 |
| `lineCount` | integer | int32 |
| `totalCountDisplay` | integer | int32 |
| `quoteRequiredCount` | integer | int32 |
| `orderSubTotal` | number | decimal |
| `orderSubTotalDisplay` | string |  |
| `orderSubTotalWithOutProductDiscounts` | number | decimal |
| `orderSubTotalWithOutProductDiscountsDisplay` | string |  |
| `totalTax` | number | decimal |
| `totalTaxDisplay` | string |  |
| `shippingAndHandling` | number | decimal |
| `shippingAndHandlingDisplay` | string |  |
| `orderGrandTotal` | number | decimal |
| `orderGrandTotalDisplay` | string |  |
| `costCodeLabel` | string |  |
| `isAuthenticated` | boolean |  |
| `isGuestOrder` | boolean |  |
| `isSalesperson` | boolean |  |
| `isSubscribed` | boolean |  |
| `requiresPoNumber` | boolean |  |
| `displayContinueShoppingLink` | boolean |  |
| `canModifyOrder` | boolean |  |
| `canSaveOrder` | boolean |  |
| `canBypassCheckoutAddress` | boolean |  |
| `canRequisition` | boolean |  |
| `canRequestQuote` | boolean |  |
| `canEditCostCode` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `showLineNotes` | boolean |  |
| `showCostCode` | boolean |  |
| `showNewsletterSignup` | boolean |  |
| `showPoNumber` | boolean |  |
| `showCreditCard` | boolean |  |
| `showECheck` | boolean |  |
| `showPayPal` | boolean |  |
| `isAwaitingApproval` | boolean |  |
| `requiresApproval` | boolean |  |
| `approverReason` | string |  |
| `hasApprover` | boolean |  |
| `salespersonName` | string |  |
| `paymentOptions` | PaymentOptionsDto |  |
| `costCodes` | CostCodeDto[] |  |
| `carriers` | CarrierDto[] |  |
| `warehouses` | WarehouseDto[] |  |
| `cartLines` | CartLineModel[] |  |
| `customerOrderTaxes` | CustomerOrderTaxDto[] |  |
| `canCheckOut` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `currencySymbol` | string |  |
| `requestedDeliveryDate` | string |  |
| `requestedDeliveryDateDisplay` | string | date-time |
| `cartNotPriced` | boolean |  |
| `messages` | string[] |  |
| `creditCardBillingAddress` | CreditCardBillingAddressDto |  |
| `alsoPurchasedProducts` | ProductDto[] |  |
| `requestedPickupDateDisplay` | string | date-time |
| `taxFailureReason` | string |  |
| `failedToGetRealTimeInventory` | boolean |  |
| `unassignCart` | boolean |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string | uuid |
| `additionalEmails` | string |  |
| `defaultWarehouse` | WarehouseModel |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/quotes/{quoteId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `quoteId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `QuoteModel` |

##### Response Schema: `QuoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `quoteLinesUri` | string |  |
| `quoteNumber` | string |  |
| `expirationDate` | string | date-time |
| `customerNumber` | string |  |
| `customerName` | string |  |
| `shipToFullAddress` | string |  |
| `quoteLineCollection` | QuoteLineModel[] |  |
| `userName` | string |  |
| `isEditable` | boolean |  |
| `messageCollection` | MessageModel[] |  |
| `calculationMethods` | CalculationMethod[] |  |
| `isJobQuote` | boolean |  |
| `jobName` | string |  |
| `cartLinesUri` | string |  |
| `id` | string |  |
| `trackId` | string |  |
| `status` | string |  |
| `statusDisplay` | string |  |
| `type` | string |  |
| `typeDisplay` | string |  |
| `orderNumber` | string |  |
| `erpOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `shipToLabel` | string |  |
| `notes` | string |  |
| `carrier` | CarrierDto |  |
| `shipVia` | ShipViaDto |  |
| `paymentMethod` | PaymentMethodDto |  |
| `fulfillmentMethod` | string |  |
| `requestedPickupDate` | string |  |
| `poNumber` | string |  |
| `promotionCode` | string |  |
| `initiatedByUserName` | string |  |
| `totalQtyOrdered` | integer | int32 |
| `lineCount` | integer | int32 |
| `totalCountDisplay` | integer | int32 |
| `quoteRequiredCount` | integer | int32 |
| `orderSubTotal` | number | decimal |
| `orderSubTotalDisplay` | string |  |
| `orderSubTotalWithOutProductDiscounts` | number | decimal |
| `orderSubTotalWithOutProductDiscountsDisplay` | string |  |
| `totalTax` | number | decimal |
| `totalTaxDisplay` | string |  |
| `shippingAndHandling` | number | decimal |
| `shippingAndHandlingDisplay` | string |  |
| `orderGrandTotal` | number | decimal |
| `orderGrandTotalDisplay` | string |  |
| `costCodeLabel` | string |  |
| `isAuthenticated` | boolean |  |
| `isGuestOrder` | boolean |  |
| `isSalesperson` | boolean |  |
| `isSubscribed` | boolean |  |
| `requiresPoNumber` | boolean |  |
| `displayContinueShoppingLink` | boolean |  |
| `canModifyOrder` | boolean |  |
| `canSaveOrder` | boolean |  |
| `canBypassCheckoutAddress` | boolean |  |
| `canRequisition` | boolean |  |
| `canRequestQuote` | boolean |  |
| `canEditCostCode` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `showLineNotes` | boolean |  |
| `showCostCode` | boolean |  |
| `showNewsletterSignup` | boolean |  |
| `showPoNumber` | boolean |  |
| `showCreditCard` | boolean |  |
| `showECheck` | boolean |  |
| `showPayPal` | boolean |  |
| `isAwaitingApproval` | boolean |  |
| `requiresApproval` | boolean |  |
| `approverReason` | string |  |
| `hasApprover` | boolean |  |
| `salespersonName` | string |  |
| `paymentOptions` | PaymentOptionsDto |  |
| `costCodes` | CostCodeDto[] |  |
| `carriers` | CarrierDto[] |  |
| `warehouses` | WarehouseDto[] |  |
| `cartLines` | CartLineModel[] |  |
| `customerOrderTaxes` | CustomerOrderTaxDto[] |  |
| `canCheckOut` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `currencySymbol` | string |  |
| `requestedDeliveryDate` | string |  |
| `requestedDeliveryDateDisplay` | string | date-time |
| `cartNotPriced` | boolean |  |
| `messages` | string[] |  |
| `creditCardBillingAddress` | CreditCardBillingAddressDto |  |
| `alsoPurchasedProducts` | ProductDto[] |  |
| `requestedPickupDateDisplay` | string | date-time |
| `taxFailureReason` | string |  |
| `failedToGetRealTimeInventory` | boolean |  |
| `unassignCart` | boolean |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string | uuid |
| `additionalEmails` | string |  |
| `defaultWarehouse` | WarehouseModel |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/quotes/{quoteId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `quoteId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `QuoteParameter`

| Property | Type | Description |
|----------|------|-------------|
| `quoteId` | string |  |
| `status` | string |  |
| `note` | string |  |
| `userId` | string | uuid |
| `expirationDate` | string | date-time |
| `calculationMethod` | integer | int32 |
| `percent` | number | double |
| `isJobQuote` | boolean |  |
| `jobName` | string |  |
| `orderQuantities` | QuoteLineModel[] |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `QuoteModel` |

##### Response Schema: `QuoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `quoteLinesUri` | string |  |
| `quoteNumber` | string |  |
| `expirationDate` | string | date-time |
| `customerNumber` | string |  |
| `customerName` | string |  |
| `shipToFullAddress` | string |  |
| `quoteLineCollection` | QuoteLineModel[] |  |
| `userName` | string |  |
| `isEditable` | boolean |  |
| `messageCollection` | MessageModel[] |  |
| `calculationMethods` | CalculationMethod[] |  |
| `isJobQuote` | boolean |  |
| `jobName` | string |  |
| `cartLinesUri` | string |  |
| `id` | string |  |
| `trackId` | string |  |
| `status` | string |  |
| `statusDisplay` | string |  |
| `type` | string |  |
| `typeDisplay` | string |  |
| `orderNumber` | string |  |
| `erpOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `shipToLabel` | string |  |
| `notes` | string |  |
| `carrier` | CarrierDto |  |
| `shipVia` | ShipViaDto |  |
| `paymentMethod` | PaymentMethodDto |  |
| `fulfillmentMethod` | string |  |
| `requestedPickupDate` | string |  |
| `poNumber` | string |  |
| `promotionCode` | string |  |
| `initiatedByUserName` | string |  |
| `totalQtyOrdered` | integer | int32 |
| `lineCount` | integer | int32 |
| `totalCountDisplay` | integer | int32 |
| `quoteRequiredCount` | integer | int32 |
| `orderSubTotal` | number | decimal |
| `orderSubTotalDisplay` | string |  |
| `orderSubTotalWithOutProductDiscounts` | number | decimal |
| `orderSubTotalWithOutProductDiscountsDisplay` | string |  |
| `totalTax` | number | decimal |
| `totalTaxDisplay` | string |  |
| `shippingAndHandling` | number | decimal |
| `shippingAndHandlingDisplay` | string |  |
| `orderGrandTotal` | number | decimal |
| `orderGrandTotalDisplay` | string |  |
| `costCodeLabel` | string |  |
| `isAuthenticated` | boolean |  |
| `isGuestOrder` | boolean |  |
| `isSalesperson` | boolean |  |
| `isSubscribed` | boolean |  |
| `requiresPoNumber` | boolean |  |
| `displayContinueShoppingLink` | boolean |  |
| `canModifyOrder` | boolean |  |
| `canSaveOrder` | boolean |  |
| `canBypassCheckoutAddress` | boolean |  |
| `canRequisition` | boolean |  |
| `canRequestQuote` | boolean |  |
| `canEditCostCode` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `showLineNotes` | boolean |  |
| `showCostCode` | boolean |  |
| `showNewsletterSignup` | boolean |  |
| `showPoNumber` | boolean |  |
| `showCreditCard` | boolean |  |
| `showECheck` | boolean |  |
| `showPayPal` | boolean |  |
| `isAwaitingApproval` | boolean |  |
| `requiresApproval` | boolean |  |
| `approverReason` | string |  |
| `hasApprover` | boolean |  |
| `salespersonName` | string |  |
| `paymentOptions` | PaymentOptionsDto |  |
| `costCodes` | CostCodeDto[] |  |
| `carriers` | CarrierDto[] |  |
| `warehouses` | WarehouseDto[] |  |
| `cartLines` | CartLineModel[] |  |
| `customerOrderTaxes` | CustomerOrderTaxDto[] |  |
| `canCheckOut` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `currencySymbol` | string |  |
| `requestedDeliveryDate` | string |  |
| `requestedDeliveryDateDisplay` | string | date-time |
| `cartNotPriced` | boolean |  |
| `messages` | string[] |  |
| `creditCardBillingAddress` | CreditCardBillingAddressDto |  |
| `alsoPurchasedProducts` | ProductDto[] |  |
| `requestedPickupDateDisplay` | string | date-time |
| `taxFailureReason` | string |  |
| `failedToGetRealTimeInventory` | boolean |  |
| `unassignCart` | boolean |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string | uuid |
| `additionalEmails` | string |  |
| `defaultWarehouse` | WarehouseModel |  |
| `properties` | object |  |

---

### `POST` /api/v1/quotes/{quoteId}/messages

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `quoteId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `MessageModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `createdDate` | string | date-time |
| `quoteId` | string | uuid |
| `message` | string |  |
| `displayName` | string |  |
| `body` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `MessageModel` |

##### Response Schema: `MessageModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `createdDate` | string | date-time |
| `quoteId` | string | uuid |
| `message` | string |  |
| `displayName` | string |  |
| `body` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/quotes/{quoteId}/quotelines/{quoteLineId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `quoteId` | string | ✅ |  |
| `quoteLineId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `QuoteLineModel` |

##### Response Schema: `QuoteLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pricingRfq` | PricingRfqModel |  |
| `maxQty` | number | decimal |
| `productUri` | string |  |
| `id` | string |  |
| `line` | integer | int32 |
| `productId` | string | uuid |
| `requisitionId` | string | uuid |
| `smallImagePath` | string |  |
| `altText` | string |  |
| `productName` | string |  |
| `manufacturerItem` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `erpNumber` | string |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `baseUnitOfMeasure` | string |  |
| `baseUnitOfMeasureDisplay` | string |  |
| `qtyPerBaseUnitOfMeasure` | number | decimal |
| `costCode` | string |  |
| `notes` | string |  |
| `qtyOrdered` | number | double |
| `qtyLeft` | number | decimal |
| `pricing` | ProductPriceDto |  |
| `isPromotionItem` | boolean |  |
| `isDiscounted` | boolean |  |
| `isConfigured` | boolean |  |
| `isFixedConfiguration` | boolean |  |
| `quoteRequired` | boolean |  |
| `breakPrices` | BreakPriceDto[] |  |
| `sectionOptions` | SectionOptionDto[] |  |
| `availability` | AvailabilityDto |  |
| `qtyOnHand` | number | decimal |
| `canAddToCart` | boolean |  |
| `isQtyAdjusted` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `salePriceLabel` | string |  |
| `cantBuy` | boolean |  |
| `isSubscription` | boolean |  |
| `productSubscription` | ProductSubscriptionDto |  |
| `isRestricted` | boolean |  |
| `canAddToWishlist` | boolean |  |
| `isActive` | boolean |  |
| `brand` | BrandDto |  |
| `vmiBinId` | string | uuid |
| `isDiscontinued` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/quotes/{quoteId}/quotelines/{quoteLineId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `quoteId` | string (uuid) | ✅ |  |
| `quoteLineId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `QuoteLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pricingRfq` | PricingRfqModel |  |
| `maxQty` | number | decimal |
| `productUri` | string |  |
| `id` | string |  |
| `line` | integer | int32 |
| `productId` | string | uuid |
| `requisitionId` | string | uuid |
| `smallImagePath` | string |  |
| `altText` | string |  |
| `productName` | string |  |
| `manufacturerItem` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `erpNumber` | string |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `baseUnitOfMeasure` | string |  |
| `baseUnitOfMeasureDisplay` | string |  |
| `qtyPerBaseUnitOfMeasure` | number | decimal |
| `costCode` | string |  |
| `notes` | string |  |
| `qtyOrdered` | number | double |
| `qtyLeft` | number | decimal |
| `pricing` | ProductPriceDto |  |
| `isPromotionItem` | boolean |  |
| `isDiscounted` | boolean |  |
| `isConfigured` | boolean |  |
| `isFixedConfiguration` | boolean |  |
| `quoteRequired` | boolean |  |
| `breakPrices` | BreakPriceDto[] |  |
| `sectionOptions` | SectionOptionDto[] |  |
| `availability` | AvailabilityDto |  |
| `qtyOnHand` | number | decimal |
| `canAddToCart` | boolean |  |
| `isQtyAdjusted` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `salePriceLabel` | string |  |
| `cantBuy` | boolean |  |
| `isSubscription` | boolean |  |
| `productSubscription` | ProductSubscriptionDto |  |
| `isRestricted` | boolean |  |
| `canAddToWishlist` | boolean |  |
| `isActive` | boolean |  |
| `brand` | BrandDto |  |
| `vmiBinId` | string | uuid |
| `isDiscontinued` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `QuoteLineModel` |

##### Response Schema: `QuoteLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pricingRfq` | PricingRfqModel |  |
| `maxQty` | number | decimal |
| `productUri` | string |  |
| `id` | string |  |
| `line` | integer | int32 |
| `productId` | string | uuid |
| `requisitionId` | string | uuid |
| `smallImagePath` | string |  |
| `altText` | string |  |
| `productName` | string |  |
| `manufacturerItem` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `erpNumber` | string |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `baseUnitOfMeasure` | string |  |
| `baseUnitOfMeasureDisplay` | string |  |
| `qtyPerBaseUnitOfMeasure` | number | decimal |
| `costCode` | string |  |
| `notes` | string |  |
| `qtyOrdered` | number | double |
| `qtyLeft` | number | decimal |
| `pricing` | ProductPriceDto |  |
| `isPromotionItem` | boolean |  |
| `isDiscounted` | boolean |  |
| `isConfigured` | boolean |  |
| `isFixedConfiguration` | boolean |  |
| `quoteRequired` | boolean |  |
| `breakPrices` | BreakPriceDto[] |  |
| `sectionOptions` | SectionOptionDto[] |  |
| `availability` | AvailabilityDto |  |
| `qtyOnHand` | number | decimal |
| `canAddToCart` | boolean |  |
| `isQtyAdjusted` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `salePriceLabel` | string |  |
| `cantBuy` | boolean |  |
| `isSubscription` | boolean |  |
| `productSubscription` | ProductSubscriptionDto |  |
| `isRestricted` | boolean |  |
| `canAddToWishlist` | boolean |  |
| `isActive` | boolean |  |
| `brand` | BrandDto |  |
| `vmiBinId` | string | uuid |
| `isDiscontinued` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `properties` | object |  |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/quotes` | GET, POST |
| `/api/v1/quotes/{quoteId}` | GET, DELETE, PATCH |
| `/api/v1/quotes/{quoteId}/quotelines/{quoteLineId}` | GET, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/quotes`
- `/api/v1/quotes/{quoteId}`

**Child / sub-resources:**

- `/api/v1/quotes/{quoteId}`
- `/api/v1/quotes/{quoteId}/messages`
- `/api/v1/quotes/{quoteId}/quotelines/{quoteLineId}`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{quoteId}`

**Linked paths:**

- `/api/v1/quotes/{quoteId}`
- `/api/v1/quotes/{quoteId}/messages`
- `/api/v1/quotes/{quoteId}/quotelines/{quoteLineId}`



---

## Jobquotes

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/jobquotes`](#get-api-v1-jobquotes)
- [`GET /api/v1/jobquotes/{jobQuoteId}`](#get-api-v1-jobquotes-jobquoteid)
- [`PATCH /api/v1/jobquotes/{jobQuoteId}`](#patch-api-v1-jobquotes-jobquoteid)

---

### `GET` /api/v1/jobquotes

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `JobQuoteCollectionModel` |

##### Response Schema: `JobQuoteCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `jobQuotes` | JobQuoteModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/jobquotes/{jobQuoteId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `jobQuoteId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `JobQuoteModel` |

##### Response Schema: `JobQuoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `jobQuoteId` | string |  |
| `isEditable` | boolean |  |
| `expirationDate` | string | date-time |
| `jobName` | string |  |
| `jobQuoteLineCollection` | JobQuoteLineModel[] |  |
| `customerName` | string |  |
| `shipToFullAddress` | string |  |
| `orderTotal` | number | decimal |
| `orderTotalDisplay` | string |  |
| `cartLinesUri` | string |  |
| `id` | string |  |
| `trackId` | string |  |
| `status` | string |  |
| `statusDisplay` | string |  |
| `type` | string |  |
| `typeDisplay` | string |  |
| `orderNumber` | string |  |
| `erpOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `shipToLabel` | string |  |
| `notes` | string |  |
| `carrier` | CarrierDto |  |
| `shipVia` | ShipViaDto |  |
| `paymentMethod` | PaymentMethodDto |  |
| `fulfillmentMethod` | string |  |
| `requestedPickupDate` | string |  |
| `poNumber` | string |  |
| `promotionCode` | string |  |
| `initiatedByUserName` | string |  |
| `totalQtyOrdered` | integer | int32 |
| `lineCount` | integer | int32 |
| `totalCountDisplay` | integer | int32 |
| `quoteRequiredCount` | integer | int32 |
| `orderSubTotal` | number | decimal |
| `orderSubTotalDisplay` | string |  |
| `orderSubTotalWithOutProductDiscounts` | number | decimal |
| `orderSubTotalWithOutProductDiscountsDisplay` | string |  |
| `totalTax` | number | decimal |
| `totalTaxDisplay` | string |  |
| `shippingAndHandling` | number | decimal |
| `shippingAndHandlingDisplay` | string |  |
| `orderGrandTotal` | number | decimal |
| `orderGrandTotalDisplay` | string |  |
| `costCodeLabel` | string |  |
| `isAuthenticated` | boolean |  |
| `isGuestOrder` | boolean |  |
| `isSalesperson` | boolean |  |
| `isSubscribed` | boolean |  |
| `requiresPoNumber` | boolean |  |
| `displayContinueShoppingLink` | boolean |  |
| `canModifyOrder` | boolean |  |
| `canSaveOrder` | boolean |  |
| `canBypassCheckoutAddress` | boolean |  |
| `canRequisition` | boolean |  |
| `canRequestQuote` | boolean |  |
| `canEditCostCode` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `showLineNotes` | boolean |  |
| `showCostCode` | boolean |  |
| `showNewsletterSignup` | boolean |  |
| `showPoNumber` | boolean |  |
| `showCreditCard` | boolean |  |
| `showECheck` | boolean |  |
| `showPayPal` | boolean |  |
| `isAwaitingApproval` | boolean |  |
| `requiresApproval` | boolean |  |
| `approverReason` | string |  |
| `hasApprover` | boolean |  |
| `salespersonName` | string |  |
| `paymentOptions` | PaymentOptionsDto |  |
| `costCodes` | CostCodeDto[] |  |
| `carriers` | CarrierDto[] |  |
| `warehouses` | WarehouseDto[] |  |
| `cartLines` | CartLineModel[] |  |
| `customerOrderTaxes` | CustomerOrderTaxDto[] |  |
| `canCheckOut` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `currencySymbol` | string |  |
| `requestedDeliveryDate` | string |  |
| `requestedDeliveryDateDisplay` | string | date-time |
| `cartNotPriced` | boolean |  |
| `messages` | string[] |  |
| `creditCardBillingAddress` | CreditCardBillingAddressDto |  |
| `alsoPurchasedProducts` | ProductDto[] |  |
| `requestedPickupDateDisplay` | string | date-time |
| `taxFailureReason` | string |  |
| `failedToGetRealTimeInventory` | boolean |  |
| `unassignCart` | boolean |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string | uuid |
| `additionalEmails` | string |  |
| `defaultWarehouse` | WarehouseModel |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/jobquotes/{jobQuoteId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `jobQuoteId` | string | ✅ |  |

#### Request Body

**Schema:** `JobQuoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `jobQuoteId` | string |  |
| `isEditable` | boolean |  |
| `expirationDate` | string | date-time |
| `jobName` | string |  |
| `jobQuoteLineCollection` | JobQuoteLineModel[] |  |
| `customerName` | string |  |
| `shipToFullAddress` | string |  |
| `orderTotal` | number | decimal |
| `orderTotalDisplay` | string |  |
| `cartLinesUri` | string |  |
| `id` | string |  |
| `trackId` | string |  |
| `status` | string |  |
| `statusDisplay` | string |  |
| `type` | string |  |
| `typeDisplay` | string |  |
| `orderNumber` | string |  |
| `erpOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `shipToLabel` | string |  |
| `notes` | string |  |
| `carrier` | CarrierDto |  |
| `shipVia` | ShipViaDto |  |
| `paymentMethod` | PaymentMethodDto |  |
| `fulfillmentMethod` | string |  |
| `requestedPickupDate` | string |  |
| `poNumber` | string |  |
| `promotionCode` | string |  |
| `initiatedByUserName` | string |  |
| `totalQtyOrdered` | integer | int32 |
| `lineCount` | integer | int32 |
| `totalCountDisplay` | integer | int32 |
| `quoteRequiredCount` | integer | int32 |
| `orderSubTotal` | number | decimal |
| `orderSubTotalDisplay` | string |  |
| `orderSubTotalWithOutProductDiscounts` | number | decimal |
| `orderSubTotalWithOutProductDiscountsDisplay` | string |  |
| `totalTax` | number | decimal |
| `totalTaxDisplay` | string |  |
| `shippingAndHandling` | number | decimal |
| `shippingAndHandlingDisplay` | string |  |
| `orderGrandTotal` | number | decimal |
| `orderGrandTotalDisplay` | string |  |
| `costCodeLabel` | string |  |
| `isAuthenticated` | boolean |  |
| `isGuestOrder` | boolean |  |
| `isSalesperson` | boolean |  |
| `isSubscribed` | boolean |  |
| `requiresPoNumber` | boolean |  |
| `displayContinueShoppingLink` | boolean |  |
| `canModifyOrder` | boolean |  |
| `canSaveOrder` | boolean |  |
| `canBypassCheckoutAddress` | boolean |  |
| `canRequisition` | boolean |  |
| `canRequestQuote` | boolean |  |
| `canEditCostCode` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `showLineNotes` | boolean |  |
| `showCostCode` | boolean |  |
| `showNewsletterSignup` | boolean |  |
| `showPoNumber` | boolean |  |
| `showCreditCard` | boolean |  |
| `showECheck` | boolean |  |
| `showPayPal` | boolean |  |
| `isAwaitingApproval` | boolean |  |
| `requiresApproval` | boolean |  |
| `approverReason` | string |  |
| `hasApprover` | boolean |  |
| `salespersonName` | string |  |
| `paymentOptions` | PaymentOptionsDto |  |
| `costCodes` | CostCodeDto[] |  |
| `carriers` | CarrierDto[] |  |
| `warehouses` | WarehouseDto[] |  |
| `cartLines` | CartLineModel[] |  |
| `customerOrderTaxes` | CustomerOrderTaxDto[] |  |
| `canCheckOut` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `currencySymbol` | string |  |
| `requestedDeliveryDate` | string |  |
| `requestedDeliveryDateDisplay` | string | date-time |
| `cartNotPriced` | boolean |  |
| `messages` | string[] |  |
| `creditCardBillingAddress` | CreditCardBillingAddressDto |  |
| `alsoPurchasedProducts` | ProductDto[] |  |
| `requestedPickupDateDisplay` | string | date-time |
| `taxFailureReason` | string |  |
| `failedToGetRealTimeInventory` | boolean |  |
| `unassignCart` | boolean |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string | uuid |
| `additionalEmails` | string |  |
| `defaultWarehouse` | WarehouseModel |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `JobQuoteModel` |

##### Response Schema: `JobQuoteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `jobQuoteId` | string |  |
| `isEditable` | boolean |  |
| `expirationDate` | string | date-time |
| `jobName` | string |  |
| `jobQuoteLineCollection` | JobQuoteLineModel[] |  |
| `customerName` | string |  |
| `shipToFullAddress` | string |  |
| `orderTotal` | number | decimal |
| `orderTotalDisplay` | string |  |
| `cartLinesUri` | string |  |
| `id` | string |  |
| `trackId` | string |  |
| `status` | string |  |
| `statusDisplay` | string |  |
| `type` | string |  |
| `typeDisplay` | string |  |
| `orderNumber` | string |  |
| `erpOrderNumber` | string |  |
| `orderDate` | string | date-time |
| `billTo` | BillToModel |  |
| `shipTo` | ShipToModel |  |
| `userLabel` | string |  |
| `userRoles` | string |  |
| `shipToLabel` | string |  |
| `notes` | string |  |
| `carrier` | CarrierDto |  |
| `shipVia` | ShipViaDto |  |
| `paymentMethod` | PaymentMethodDto |  |
| `fulfillmentMethod` | string |  |
| `requestedPickupDate` | string |  |
| `poNumber` | string |  |
| `promotionCode` | string |  |
| `initiatedByUserName` | string |  |
| `totalQtyOrdered` | integer | int32 |
| `lineCount` | integer | int32 |
| `totalCountDisplay` | integer | int32 |
| `quoteRequiredCount` | integer | int32 |
| `orderSubTotal` | number | decimal |
| `orderSubTotalDisplay` | string |  |
| `orderSubTotalWithOutProductDiscounts` | number | decimal |
| `orderSubTotalWithOutProductDiscountsDisplay` | string |  |
| `totalTax` | number | decimal |
| `totalTaxDisplay` | string |  |
| `shippingAndHandling` | number | decimal |
| `shippingAndHandlingDisplay` | string |  |
| `orderGrandTotal` | number | decimal |
| `orderGrandTotalDisplay` | string |  |
| `costCodeLabel` | string |  |
| `isAuthenticated` | boolean |  |
| `isGuestOrder` | boolean |  |
| `isSalesperson` | boolean |  |
| `isSubscribed` | boolean |  |
| `requiresPoNumber` | boolean |  |
| `displayContinueShoppingLink` | boolean |  |
| `canModifyOrder` | boolean |  |
| `canSaveOrder` | boolean |  |
| `canBypassCheckoutAddress` | boolean |  |
| `canRequisition` | boolean |  |
| `canRequestQuote` | boolean |  |
| `canEditCostCode` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `showLineNotes` | boolean |  |
| `showCostCode` | boolean |  |
| `showNewsletterSignup` | boolean |  |
| `showPoNumber` | boolean |  |
| `showCreditCard` | boolean |  |
| `showECheck` | boolean |  |
| `showPayPal` | boolean |  |
| `isAwaitingApproval` | boolean |  |
| `requiresApproval` | boolean |  |
| `approverReason` | string |  |
| `hasApprover` | boolean |  |
| `salespersonName` | string |  |
| `paymentOptions` | PaymentOptionsDto |  |
| `costCodes` | CostCodeDto[] |  |
| `carriers` | CarrierDto[] |  |
| `warehouses` | WarehouseDto[] |  |
| `cartLines` | CartLineModel[] |  |
| `customerOrderTaxes` | CustomerOrderTaxDto[] |  |
| `canCheckOut` | boolean |  |
| `hasInsufficientInventory` | boolean |  |
| `currencySymbol` | string |  |
| `requestedDeliveryDate` | string |  |
| `requestedDeliveryDateDisplay` | string | date-time |
| `cartNotPriced` | boolean |  |
| `messages` | string[] |  |
| `creditCardBillingAddress` | CreditCardBillingAddressDto |  |
| `alsoPurchasedProducts` | ProductDto[] |  |
| `requestedPickupDateDisplay` | string | date-time |
| `taxFailureReason` | string |  |
| `failedToGetRealTimeInventory` | boolean |  |
| `unassignCart` | boolean |  |
| `customerVatNumber` | string |  |
| `vmiLocationId` | string | uuid |
| `additionalEmails` | string |  |
| `defaultWarehouse` | WarehouseModel |  |
| `properties` | object |  |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/jobquotes/{jobQuoteId}` | GET, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/jobquotes`

**Child / sub-resources:**

- `/api/v1/jobquotes/{jobQuoteId}`



---

## Invoices

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/invoices`](#get-api-v1-invoices)
- [`GET /api/v1/invoices/{invoiceId}`](#get-api-v1-invoices-invoiceid)
- [`POST /api/v1/invoices/shareinvoice`](#post-api-v1-invoices-shareinvoice)

---

### `GET` /api/v1/invoices

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.customerSequence` | string | ❌ |  |
| `parameter.invoiceNumber` | string | ❌ |  |
| `parameter.orderNumber` | string | ❌ |  |
| `parameter.fromDate` | string (date-time) | ❌ |  |
| `parameter.toDate` | string (date-time) | ❌ |  |
| `parameter.showOpenOnly` | boolean | ❌ |  |
| `parameter.statusCollection` | string[] | ❌ |  |
| `parameter.invoiceTotalOperator` | string | ❌ |  |
| `parameter.poNumber` | string | ❌ |  |
| `parameter.terms` | string | ❌ |  |
| `parameter.currentPage` | integer (int32) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `InvoiceCollectionModel` |

##### Response Schema: `InvoiceCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `invoices` | InvoiceModel[] |  |
| `pagination` | PaginationModel |  |
| `showErpOrderNumber` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/invoices/{invoiceId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `invoiceId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `InvoiceModel` |

##### Response Schema: `InvoiceModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `invoiceNumber` | string |  |
| `invoiceDate` | string | date-time |
| `dueDate` | string | date-time |
| `invoiceType` | string |  |
| `customerNumber` | string |  |
| `customerSequence` | string |  |
| `customerPO` | string |  |
| `status` | string |  |
| `isOpen` | boolean |  |
| `currencyCode` | string |  |
| `terms` | string |  |
| `shipCode` | string |  |
| `salesperson` | string |  |
| `btCompanyName` | string |  |
| `btAddress1` | string |  |
| `btAddress2` | string |  |
| `billToCity` | string |  |
| `billToState` | string |  |
| `billToPostalCode` | string |  |
| `btCountry` | string |  |
| `stCompanyName` | string |  |
| `stAddress1` | string |  |
| `stAddress2` | string |  |
| `shipToCity` | string |  |
| `shipToState` | string |  |
| `shipToPostalCode` | string |  |
| `stCountry` | string |  |
| `notes` | string |  |
| `productTotal` | number | decimal |
| `discountAmount` | number | decimal |
| `shippingAndHandling` | number | decimal |
| `otherCharges` | number | decimal |
| `taxAmount` | number | decimal |
| `invoiceTotal` | number | decimal |
| `currentBalance` | number | decimal |
| `invoiceLines` | InvoiceLineModel[] |  |
| `invoiceHistoryTaxes` | InvoiceHistoryTaxDto[] |  |
| `invoiceTotalDisplay` | string |  |
| `productTotalDisplay` | string |  |
| `discountAmountDisplay` | string |  |
| `taxAmountDisplay` | string |  |
| `shippingAndHandlingDisplay` | string |  |
| `otherChargesDisplay` | string |  |
| `currentBalanceDisplay` | string |  |
| `orderTotalDisplay` | string |  |
| `shipViaDescription` | string |  |
| `customerVatNumber` | string |  |
| `properties` | object |  |

---

### `POST` /api/v1/invoices/shareinvoice

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `ShareEntityModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `emailTo` | string |  |
| `emailFrom` | string |  |
| `subject` | string |  |
| `message` | string |  |
| `entityId` | string |  |
| `entityName` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ShareEntityModel` |

##### Response Schema: `ShareEntityModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `emailTo` | string |  |
| `emailFrom` | string |  |
| `subject` | string |  |
| `message` | string |  |
| `entityId` | string |  |
| `entityName` | string |  |
| `properties` | object |  |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/invoices`

**Child / sub-resources:**

- `/api/v1/invoices/shareinvoice`
- `/api/v1/invoices/{invoiceId}`

#### Shared Models

These response/request models are also used by other API sections:

| Model | Also used in |
|-------|--------------|
| `ShareEntityModel` | Orders |



---

## Orderfeed

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/orderfeed`](#get-api-v1-orderfeed)

---

### `GET` /api/v1/orderfeed

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

## Orderstatusmappings

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/orderstatusmappings`](#get-api-v1-orderstatusmappings)

---

### `GET` /api/v1/orderstatusmappings

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `OrderStatusMappingCollectionModel` |

##### Response Schema: `OrderStatusMappingCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `orderStatusMappings` | OrderStatusMappingModel[] |  |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

