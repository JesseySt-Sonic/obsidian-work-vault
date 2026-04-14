---
tags:
  - storefront-api
---

# Commerce & Checkout

Shopping cart lifecycle, promotions, wishlists, and requisitions. The `{cartId}` and `{wishListId}` path parameters are the key pivots linking this service to Orders and Identity.

---

## Contents

- [[#Carts]]
- [[#Wishlists]]
- [[#Requisitions]]

---

## Carts

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/carts/{cartId}/promotions`](#get-api-v1-carts-cartid-promotions)
- [`POST /api/v1/carts/{cartId}/promotions`](#post-api-v1-carts-cartid-promotions)
- [`DELETE /api/v1/carts/{cartId}/promotions`](#delete-api-v1-carts-cartid-promotions)
- [`GET /api/v1/carts/{cartId}/promotions/{promotionId}`](#get-api-v1-carts-cartid-promotions-promotionid)
- [`DELETE /api/v1/carts/{cartId}/promotions/{promotionId}`](#delete-api-v1-carts-cartid-promotions-promotionid)
- [`GET /api/v1/carts`](#get-api-v1-carts)
- [`POST /api/v1/carts`](#post-api-v1-carts)
- [`GET /api/v1/carts/{cartId}`](#get-api-v1-carts-cartid)
- [`DELETE /api/v1/carts/{cartId}`](#delete-api-v1-carts-cartid)
- [`PATCH /api/v1/carts/{cartId}`](#patch-api-v1-carts-cartid)
- [`GET /api/v1/carts/{cartId}/cartlines/{cartLineId}`](#get-api-v1-carts-cartid-cartlines-cartlineid)
- [`DELETE /api/v1/carts/{cartId}/cartlines/{cartLineId}`](#delete-api-v1-carts-cartid-cartlines-cartlineid)
- [`PATCH /api/v1/carts/{cartId}/cartlines/{cartLineId}`](#patch-api-v1-carts-cartid-cartlines-cartlineid)
- [`POST /api/v1/carts/{cartId}/cartlines/batch`](#post-api-v1-carts-cartid-cartlines-batch)
- [`POST /api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}`](#post-api-v1-carts-cartid-cartlines-wishlist-wishlistid)
- [`POST /api/v1/carts/{cartId}/cartlines`](#post-api-v1-carts-cartid-cartlines)
- [`DELETE /api/v1/carts/{cartId}/cartlines`](#delete-api-v1-carts-cartid-cartlines)

---

### `GET` /api/v1/carts/{cartId}/promotions

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `PromotionCollectionModel` |

##### Response Schema: `PromotionCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `promotions` | PromotionModel[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/carts/{cartId}/promotions

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |

#### Request Body

**Schema:** `PromotionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `promotionCode` | string |  |
| `name` | string |  |
| `amount` | number | decimal |
| `amountDisplay` | string |  |
| `promotionApplied` | boolean |  |
| `message` | string |  |
| `orderLineId` | string | uuid |
| `promotionResultType` | string |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `PromotionModel` |

##### Response Schema: `PromotionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `promotionCode` | string |  |
| `name` | string |  |
| `amount` | number | decimal |
| `amountDisplay` | string |  |
| `promotionApplied` | boolean |  |
| `message` | string |  |
| `orderLineId` | string | uuid |
| `promotionResultType` | string |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/carts/{cartId}/promotions

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `PromotionCollectionModel` |

##### Response Schema: `PromotionCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `promotions` | PromotionModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/carts/{cartId}/promotions/{promotionId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |
| `promotionId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `PromotionModel` |

##### Response Schema: `PromotionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `promotionCode` | string |  |
| `name` | string |  |
| `amount` | number | decimal |
| `amountDisplay` | string |  |
| `promotionApplied` | boolean |  |
| `message` | string |  |
| `orderLineId` | string | uuid |
| `promotionResultType` | string |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/carts/{cartId}/promotions/{promotionId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |
| `promotionId` | string (uuid) | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `PromotionModel` |

##### Response Schema: `PromotionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `promotionCode` | string |  |
| `name` | string |  |
| `amount` | number | decimal |
| `amountDisplay` | string |  |
| `promotionApplied` | boolean |  |
| `message` | string |  |
| `orderLineId` | string | uuid |
| `promotionResultType` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/carts

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.billToId` | string (uuid) | ❌ |  |
| `parameter.shipToId` | string (uuid) | ❌ |  |
| `parameter.status` | string | ❌ |  |
| `parameter.orderNumber` | string | ❌ |  |
| `parameter.fromDate` | string (date-time) | ❌ |  |
| `parameter.toDate` | string (date-time) | ❌ |  |
| `parameter.orderTotalOperator` | string | ❌ |  |
| `parameter.orderTotal` | number (decimal) | ❌ |  |
| `parameter.orderSubtotalOperator` | string | ❌ |  |
| `parameter.orderSubtotal` | number (decimal) | ❌ |  |
| `parameter.vmiLocationId` | string (uuid) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CartCollectionModel` |

##### Response Schema: `CartCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `carts` | CartModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `POST` /api/v1/carts

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `AddCartModel`

| Property | Type | Description |
|----------|------|-------------|
| `billToId` | string | uuid |
| `shipToId` | string | uuid |
| `notes` | string |  |
| `vmiLocationId` | string | uuid |

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

### `GET` /api/v1/carts/{cartId}

**Auth required:** ❌ No

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

### `DELETE` /api/v1/carts/{cartId}

**Auth required:** ❌ No

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

### `PATCH` /api/v1/carts/{cartId}

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |

#### Request Body

**Schema:** `CartModel`

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

### `GET` /api/v1/carts/{cartId}/cartlines/{cartLineId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |
| `cartLineId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CartLineModel` |

##### Response Schema: `CartLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
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

### `DELETE` /api/v1/carts/{cartId}/cartlines/{cartLineId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |
| `cartLineId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CartLineModel` |

##### Response Schema: `CartLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
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

### `PATCH` /api/v1/carts/{cartId}/cartlines/{cartLineId}

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |
| `cartLineId` | string | ✅ |  |

#### Request Body

**Schema:** `CartLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
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
| `200` | OK | `CartLineModel` |

##### Response Schema: `CartLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
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

### `POST` /api/v1/carts/{cartId}/cartlines/batch

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |

#### Request Body

**Schema:** `CartLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `cartLines` | CartLineModel[] |  |
| `pagination` | PaginationModel |  |
| `notAllAddedToCart` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CartLineCollectionModel` |

##### Response Schema: `CartLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `cartLines` | CartLineModel[] |  |
| `pagination` | PaginationModel |  |
| `notAllAddedToCart` | boolean |  |
| `properties` | object |  |

---

### `POST` /api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |
| `wishListId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `AddWishListToCartModel`

| Property | Type | Description |
|----------|------|-------------|
| `cartId` | string | uuid |
| `wishListId` | string | uuid |
| `changedSharedListLinesQuantities` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CartLineCollectionModel` |

##### Response Schema: `CartLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `cartLines` | CartLineModel[] |  |
| `pagination` | PaginationModel |  |
| `notAllAddedToCart` | boolean |  |
| `properties` | object |  |

---

### `POST` /api/v1/carts/{cartId}/cartlines

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `cartId` | string | ✅ |  |

#### Request Body

**Schema:** `CartLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
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
| `200` | OK | `CartLineModel` |

##### Response Schema: `CartLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
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

### `DELETE` /api/v1/carts/{cartId}/cartlines

**Auth required:** ❌ No

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

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/carts` | GET, POST |
| `/api/v1/carts/{cartId}` | GET, DELETE, PATCH |
| `/api/v1/carts/{cartId}/cartlines` | POST, DELETE |
| `/api/v1/carts/{cartId}/cartlines/{cartLineId}` | GET, DELETE, PATCH |
| `/api/v1/carts/{cartId}/promotions` | GET, POST, DELETE |
| `/api/v1/carts/{cartId}/promotions/{promotionId}` | GET, DELETE |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/carts`
- `/api/v1/carts/{cartId}`
- `/api/v1/carts/{cartId}/cartlines`
- `/api/v1/carts/{cartId}/promotions`

**Child / sub-resources:**

- `/api/v1/carts/{cartId}`
- `/api/v1/carts/{cartId}/cartlines`
- `/api/v1/carts/{cartId}/promotions`
- `/api/v1/carts/{cartId}/cartlines/batch`
- `/api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}`
- `/api/v1/carts/{cartId}/cartlines/{cartLineId}`
- `/api/v1/carts/{cartId}/promotions/{promotionId}`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{cartId}`

**Also used in tags:** Orderapprovals  
**Linked paths:**

- `/api/v1/carts/{cartId}`
- `/api/v1/carts/{cartId}/cartlines`
- `/api/v1/carts/{cartId}/cartlines/batch`
- `/api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}`
- `/api/v1/carts/{cartId}/cartlines/{cartLineId}`
- `/api/v1/carts/{cartId}/promotions`
- `/api/v1/carts/{cartId}/promotions/{promotionId}`
- `/api/v1/orderapprovals/{cartId}`

##### `{wishListId}`

**Also used in tags:** Wishlists  
**Linked paths:**

- `/api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}`
- `/api/v1/wishlists/{wishListId}`
- `/api/v1/wishlists/{wishListId}/schedule`
- `/api/v1/wishlists/{wishListId}/send-pdf`
- `/api/v1/wishlists/{wishListId}/sendacopy`
- `/api/v1/wishlists/{wishListId}/share/{wishListShareId}`
- `/api/v1/wishlists/{wishListId}/tags/batch`
- `/api/v1/wishlists/{wishListId}/wishlistlines`
- `/api/v1/wishlists/{wishListId}/wishlistlines/batch`
- `/api/v1/wishlists/{wishListId}/wishlistlines/batch/{copyFromWishListId}`
- `/api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}`

#### Shared Models

These response/request models are also used by other API sections:

| Model | Also used in |
|-------|--------------|
| `CartModel` | Orderapprovals |



---

## Wishlists

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}`](#get-api-v1-wishlists-wishlistid-wishlistlines-wishlistlineid)
- [`DELETE /api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}`](#delete-api-v1-wishlists-wishlistid-wishlistlines-wishlistlineid)
- [`PATCH /api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}`](#patch-api-v1-wishlists-wishlistid-wishlistlines-wishlistlineid)
- [`POST /api/v1/wishlists/{wishListId}/wishlistlines/batch/{copyFromWishListId}`](#post-api-v1-wishlists-wishlistid-wishlistlines-batch-copyfromwishlistid)
- [`DELETE /api/v1/wishlists/{wishListId}/wishlistlines/batch`](#delete-api-v1-wishlists-wishlistid-wishlistlines-batch)
- [`PATCH /api/v1/wishlists/{wishListId}/wishlistlines/batch`](#patch-api-v1-wishlists-wishlistid-wishlistlines-batch)
- [`GET /api/v1/wishlists/{wishListId}/wishlistlines`](#get-api-v1-wishlists-wishlistid-wishlistlines)
- [`POST /api/v1/wishlists/{wishListId}/wishlistlines`](#post-api-v1-wishlists-wishlistid-wishlistlines)
- [`GET /api/v1/wishlists`](#get-api-v1-wishlists)
- [`POST /api/v1/wishlists`](#post-api-v1-wishlists)
- [`GET /api/v1/wishlists/{wishListId}`](#get-api-v1-wishlists-wishlistid)
- [`DELETE /api/v1/wishlists/{wishListId}`](#delete-api-v1-wishlists-wishlistid)
- [`PATCH /api/v1/wishlists/{wishListId}`](#patch-api-v1-wishlists-wishlistid)
- [`DELETE /api/v1/wishlists/{wishListId}/share/{wishListShareId}`](#delete-api-v1-wishlists-wishlistid-share-wishlistshareid)
- [`PATCH /api/v1/wishlists/activateinvite`](#patch-api-v1-wishlists-activateinvite)
- [`PATCH /api/v1/wishlists/{wishListId}/sendacopy`](#patch-api-v1-wishlists-wishlistid-sendacopy)
- [`PATCH /api/v1/wishlists/{wishListId}/schedule`](#patch-api-v1-wishlists-wishlistid-schedule)
- [`POST /api/v1/wishlists/{wishListId}/tags/batch`](#post-api-v1-wishlists-wishlistid-tags-batch)
- [`DELETE /api/v1/wishlists/{wishListId}/tags/batch`](#delete-api-v1-wishlists-wishlistid-tags-batch)
- [`POST /api/v1/wishlists/{wishListId}/send-pdf`](#post-api-v1-wishlists-wishlistid-send-pdf)

---

### `GET` /api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |
| `wishListLineId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListLineModel` |

##### Response Schema: `WishListLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `productUri` | string |  |
| `productId` | string | uuid |
| `smallImagePath` | string |  |
| `altText` | string |  |
| `productName` | string |  |
| `manufacturerItem` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `qtyOnHand` | number | decimal |
| `qtyOrdered` | number | decimal |
| `erpNumber` | string |  |
| `pricing` | ProductPriceDto |  |
| `quoteRequired` | boolean |  |
| `isActive` | boolean |  |
| `canEnterQuantity` | boolean |  |
| `canShowPrice` | boolean |  |
| `canAddToCart` | boolean |  |
| `canShowUnitOfMeasure` | boolean |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `availability` | AvailabilityDto |  |
| `breakPrices` | BreakPriceDto[] |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `baseUnitOfMeasure` | string |  |
| `baseUnitOfMeasureDisplay` | string |  |
| `qtyPerBaseUnitOfMeasure` | number | decimal |
| `selectedUnitOfMeasure` | string |  |
| `productUnitOfMeasures` | ProductUnitOfMeasureDto[] |  |
| `packDescription` | string |  |
| `createdOn` | string | date-time |
| `notes` | string |  |
| `createdByDisplayName` | string |  |
| `isSharedLine` | boolean |  |
| `isVisible` | boolean |  |
| `isDiscontinued` | boolean |  |
| `sortOrder` | integer | int32 |
| `brand` | BrandDto |  |
| `isQtyAdjusted` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `badges` | BadgeDto[] |  |
| `replacementProduct` | ProductDto |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |
| `wishListLineId` | string (uuid) | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListLineModel` |

##### Response Schema: `WishListLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `productUri` | string |  |
| `productId` | string | uuid |
| `smallImagePath` | string |  |
| `altText` | string |  |
| `productName` | string |  |
| `manufacturerItem` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `qtyOnHand` | number | decimal |
| `qtyOrdered` | number | decimal |
| `erpNumber` | string |  |
| `pricing` | ProductPriceDto |  |
| `quoteRequired` | boolean |  |
| `isActive` | boolean |  |
| `canEnterQuantity` | boolean |  |
| `canShowPrice` | boolean |  |
| `canAddToCart` | boolean |  |
| `canShowUnitOfMeasure` | boolean |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `availability` | AvailabilityDto |  |
| `breakPrices` | BreakPriceDto[] |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `baseUnitOfMeasure` | string |  |
| `baseUnitOfMeasureDisplay` | string |  |
| `qtyPerBaseUnitOfMeasure` | number | decimal |
| `selectedUnitOfMeasure` | string |  |
| `productUnitOfMeasures` | ProductUnitOfMeasureDto[] |  |
| `packDescription` | string |  |
| `createdOn` | string | date-time |
| `notes` | string |  |
| `createdByDisplayName` | string |  |
| `isSharedLine` | boolean |  |
| `isVisible` | boolean |  |
| `isDiscontinued` | boolean |  |
| `sortOrder` | integer | int32 |
| `brand` | BrandDto |  |
| `isQtyAdjusted` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `badges` | BadgeDto[] |  |
| `replacementProduct` | ProductDto |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |
| `wishListLineId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `WishListLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `productUri` | string |  |
| `productId` | string | uuid |
| `smallImagePath` | string |  |
| `altText` | string |  |
| `productName` | string |  |
| `manufacturerItem` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `qtyOnHand` | number | decimal |
| `qtyOrdered` | number | decimal |
| `erpNumber` | string |  |
| `pricing` | ProductPriceDto |  |
| `quoteRequired` | boolean |  |
| `isActive` | boolean |  |
| `canEnterQuantity` | boolean |  |
| `canShowPrice` | boolean |  |
| `canAddToCart` | boolean |  |
| `canShowUnitOfMeasure` | boolean |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `availability` | AvailabilityDto |  |
| `breakPrices` | BreakPriceDto[] |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `baseUnitOfMeasure` | string |  |
| `baseUnitOfMeasureDisplay` | string |  |
| `qtyPerBaseUnitOfMeasure` | number | decimal |
| `selectedUnitOfMeasure` | string |  |
| `productUnitOfMeasures` | ProductUnitOfMeasureDto[] |  |
| `packDescription` | string |  |
| `createdOn` | string | date-time |
| `notes` | string |  |
| `createdByDisplayName` | string |  |
| `isSharedLine` | boolean |  |
| `isVisible` | boolean |  |
| `isDiscontinued` | boolean |  |
| `sortOrder` | integer | int32 |
| `brand` | BrandDto |  |
| `isQtyAdjusted` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `badges` | BadgeDto[] |  |
| `replacementProduct` | ProductDto |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListLineModel` |

##### Response Schema: `WishListLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `productUri` | string |  |
| `productId` | string | uuid |
| `smallImagePath` | string |  |
| `altText` | string |  |
| `productName` | string |  |
| `manufacturerItem` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `qtyOnHand` | number | decimal |
| `qtyOrdered` | number | decimal |
| `erpNumber` | string |  |
| `pricing` | ProductPriceDto |  |
| `quoteRequired` | boolean |  |
| `isActive` | boolean |  |
| `canEnterQuantity` | boolean |  |
| `canShowPrice` | boolean |  |
| `canAddToCart` | boolean |  |
| `canShowUnitOfMeasure` | boolean |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `availability` | AvailabilityDto |  |
| `breakPrices` | BreakPriceDto[] |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `baseUnitOfMeasure` | string |  |
| `baseUnitOfMeasureDisplay` | string |  |
| `qtyPerBaseUnitOfMeasure` | number | decimal |
| `selectedUnitOfMeasure` | string |  |
| `productUnitOfMeasures` | ProductUnitOfMeasureDto[] |  |
| `packDescription` | string |  |
| `createdOn` | string | date-time |
| `notes` | string |  |
| `createdByDisplayName` | string |  |
| `isSharedLine` | boolean |  |
| `isVisible` | boolean |  |
| `isDiscontinued` | boolean |  |
| `sortOrder` | integer | int32 |
| `brand` | BrandDto |  |
| `isQtyAdjusted` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `badges` | BadgeDto[] |  |
| `replacementProduct` | ProductDto |  |
| `properties` | object |  |

---

### `POST` /api/v1/wishlists/{wishListId}/wishlistlines/batch/{copyFromWishListId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string | ✅ |  |
| `copyFromWishListId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `WishListLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLines` | WishListLineModel[] |  |
| `changedListLineQuantities` | object |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListLineCollectionModel` |

##### Response Schema: `WishListLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLines` | WishListLineModel[] |  |
| `changedListLineQuantities` | object |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/wishlists/{wishListId}/wishlistlines/batch

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListLineIds` | string[] | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListLineCollectionModel` |

##### Response Schema: `WishListLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLines` | WishListLineModel[] |  |
| `changedListLineQuantities` | object |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/wishlists/{wishListId}/wishlistlines/batch

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string | ✅ |  |

#### Request Body

**Schema:** `UpdateWishListLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListId` | string | uuid |
| `changedSharedListLinesQuantities` | object |  |
| `includeListLines` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListLineCollectionModel` |

##### Response Schema: `WishListLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLines` | WishListLineModel[] |  |
| `changedListLineQuantities` | object |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/wishlists/{wishListId}/wishlistlines

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.wishListId` | string (uuid) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.defaultPageSize` | integer (int32) | ❌ |  |
| `parameter.query` | string | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.changedSharedListLinesQuantities` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListLineCollectionModel` |

##### Response Schema: `WishListLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLines` | WishListLineModel[] |  |
| `changedListLineQuantities` | object |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `POST` /api/v1/wishlists/{wishListId}/wishlistlines

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `WishListLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `productUri` | string |  |
| `productId` | string | uuid |
| `smallImagePath` | string |  |
| `altText` | string |  |
| `productName` | string |  |
| `manufacturerItem` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `qtyOnHand` | number | decimal |
| `qtyOrdered` | number | decimal |
| `erpNumber` | string |  |
| `pricing` | ProductPriceDto |  |
| `quoteRequired` | boolean |  |
| `isActive` | boolean |  |
| `canEnterQuantity` | boolean |  |
| `canShowPrice` | boolean |  |
| `canAddToCart` | boolean |  |
| `canShowUnitOfMeasure` | boolean |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `availability` | AvailabilityDto |  |
| `breakPrices` | BreakPriceDto[] |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `baseUnitOfMeasure` | string |  |
| `baseUnitOfMeasureDisplay` | string |  |
| `qtyPerBaseUnitOfMeasure` | number | decimal |
| `selectedUnitOfMeasure` | string |  |
| `productUnitOfMeasures` | ProductUnitOfMeasureDto[] |  |
| `packDescription` | string |  |
| `createdOn` | string | date-time |
| `notes` | string |  |
| `createdByDisplayName` | string |  |
| `isSharedLine` | boolean |  |
| `isVisible` | boolean |  |
| `isDiscontinued` | boolean |  |
| `sortOrder` | integer | int32 |
| `brand` | BrandDto |  |
| `isQtyAdjusted` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `badges` | BadgeDto[] |  |
| `replacementProduct` | ProductDto |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListLineModel` |

##### Response Schema: `WishListLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `productUri` | string |  |
| `productId` | string | uuid |
| `smallImagePath` | string |  |
| `altText` | string |  |
| `productName` | string |  |
| `manufacturerItem` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `qtyOnHand` | number | decimal |
| `qtyOrdered` | number | decimal |
| `erpNumber` | string |  |
| `pricing` | ProductPriceDto |  |
| `quoteRequired` | boolean |  |
| `isActive` | boolean |  |
| `canEnterQuantity` | boolean |  |
| `canShowPrice` | boolean |  |
| `canAddToCart` | boolean |  |
| `canShowUnitOfMeasure` | boolean |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `availability` | AvailabilityDto |  |
| `breakPrices` | BreakPriceDto[] |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `baseUnitOfMeasure` | string |  |
| `baseUnitOfMeasureDisplay` | string |  |
| `qtyPerBaseUnitOfMeasure` | number | decimal |
| `selectedUnitOfMeasure` | string |  |
| `productUnitOfMeasures` | ProductUnitOfMeasureDto[] |  |
| `packDescription` | string |  |
| `createdOn` | string | date-time |
| `notes` | string |  |
| `createdByDisplayName` | string |  |
| `isSharedLine` | boolean |  |
| `isVisible` | boolean |  |
| `isDiscontinued` | boolean |  |
| `sortOrder` | integer | int32 |
| `brand` | BrandDto |  |
| `isQtyAdjusted` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `badges` | BadgeDto[] |  |
| `replacementProduct` | ProductDto |  |
| `properties` | object |  |

---

### `GET` /api/v1/wishlists

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListCollectionModel` |

##### Response Schema: `WishListCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListCollection` | WishListModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `POST` /api/v1/wishlists

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListModel` |

##### Response Schema: `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/wishlists/{wishListId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.wishListId` | string (uuid) | ❌ |  |
| `parameter.expand` | string | ❌ |  |
| `parameter.exclude` | string | ❌ |  |
| `parameter.currentPage` | integer (int32) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListModel` |

##### Response Schema: `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/wishlists/{wishListId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListModel` |

##### Response Schema: `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/wishlists/{wishListId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListModel` |

##### Response Schema: `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/wishlists/{wishListId}/share/{wishListShareId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |
| `wishListShareId` | string (uuid) | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListModel` |

##### Response Schema: `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/wishlists/activateinvite

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `WishListInviteParameter`

| Property | Type | Description |
|----------|------|-------------|
| `invite` | string |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListModel` |

##### Response Schema: `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/wishlists/{wishListId}/sendacopy

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListModel` |

##### Response Schema: `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

---

### `PATCH` /api/v1/wishlists/{wishListId}/schedule

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListModel` |

##### Response Schema: `WishListModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListLinesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `canAddAllToCart` | boolean |  |
| `canAddToCart` | boolean |  |
| `hasAnyLines` | boolean |  |
| `description` | string |  |
| `updatedOn` | string | date-time |
| `updatedByDisplayName` | string |  |
| `wishListLinesCount` | integer | int32 |
| `wishListSharesCount` | integer | int32 |
| `isSharedList` | boolean |  |
| `sharedByDisplayName` | string |  |
| `sharedByUserName` | string |  |
| `sharedUsers` | WishListShareModel[] |  |
| `pagination` | PaginationModel |  |
| `wishListLineCollection` | WishListLineModel[] |  |
| `allowEdit` | boolean |  |
| `shareOption` | string |  |
| `recipientEmailAddress` | string |  |
| `sendEmail` | boolean |  |
| `message` | string |  |
| `senderName` | string |  |
| `schedule` | WishListEmailScheduleModel |  |
| `sendDayOfWeekPossibleValues` | string[] |  |
| `sendDayOfMonthPossibleValues` | string[] |  |
| `isGlobal` | boolean |  |
| `isAutogenerated` | boolean |  |
| `isFavorite` | boolean |  |
| `isHidden` | boolean |  |
| `wishListTags` | WishListTagModel[] |  |
| `isDynamic` | boolean |  |
| `properties` | object |  |

---

### `POST` /api/v1/wishlists/{wishListId}/tags/batch

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `WishListTagCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListTags` | WishListTagModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListTagCollectionModel` |

##### Response Schema: `WishListTagCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListTags` | WishListTagModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/wishlists/{wishListId}/tags/batch

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListTagIds` | string[] | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListTagCollectionModel` |

##### Response Schema: `WishListTagCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `wishListTags` | WishListTagModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `POST` /api/v1/wishlists/{wishListId}/send-pdf

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `wishListId` | string (uuid) | ✅ |  |

#### Request Body

**Schema:** `WishListPdfParameter`

| Property | Type | Description |
|----------|------|-------------|
| `lineIds` | string[] |  |
| `layout` | string |  |
| `barcodeFormat` | string |  |
| `barcodeField` | string |  |
| `displayFields` | string[] |  |
| `addOverlay` | boolean |  |
| `wishListId` | string | uuid |
| `page` | integer | int32 |
| `pageSize` | integer | int32 |
| `defaultPageSize` | integer | int32 |
| `query` | string |  |
| `sort` | string |  |
| `changedSharedListLinesQuantities` | string |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListPdfModel` |

##### Response Schema: `WishListPdfModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `properties` | object |  |

---


---

### Relationships

#### CRUD Operations

The following paths support multiple HTTP methods:

| Path | Methods |
|------|---------|
| `/api/v1/wishlists` | GET, POST |
| `/api/v1/wishlists/{wishListId}` | GET, DELETE, PATCH |
| `/api/v1/wishlists/{wishListId}/tags/batch` | POST, DELETE |
| `/api/v1/wishlists/{wishListId}/wishlistlines` | GET, POST |
| `/api/v1/wishlists/{wishListId}/wishlistlines/batch` | DELETE, PATCH |
| `/api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}` | GET, DELETE, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/wishlists`
- `/api/v1/wishlists/{wishListId}`
- `/api/v1/wishlists/{wishListId}/wishlistlines`
- `/api/v1/wishlists/{wishListId}/wishlistlines/batch`

**Child / sub-resources:**

- `/api/v1/wishlists/activateinvite`
- `/api/v1/wishlists/{wishListId}`
- `/api/v1/wishlists/{wishListId}/schedule`
- `/api/v1/wishlists/{wishListId}/send-pdf`
- `/api/v1/wishlists/{wishListId}/sendacopy`
- `/api/v1/wishlists/{wishListId}/share/{wishListShareId}`
- `/api/v1/wishlists/{wishListId}/tags/batch`
- `/api/v1/wishlists/{wishListId}/wishlistlines`
- `/api/v1/wishlists/{wishListId}/wishlistlines/batch`
- `/api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}`
- `/api/v1/wishlists/{wishListId}/wishlistlines/batch/{copyFromWishListId}`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{wishListId}`

**Also used in tags:** Carts  
**Linked paths:**

- `/api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}`
- `/api/v1/wishlists/{wishListId}`
- `/api/v1/wishlists/{wishListId}/schedule`
- `/api/v1/wishlists/{wishListId}/send-pdf`
- `/api/v1/wishlists/{wishListId}/sendacopy`
- `/api/v1/wishlists/{wishListId}/share/{wishListShareId}`
- `/api/v1/wishlists/{wishListId}/tags/batch`
- `/api/v1/wishlists/{wishListId}/wishlistlines`
- `/api/v1/wishlists/{wishListId}/wishlistlines/batch`
- `/api/v1/wishlists/{wishListId}/wishlistlines/batch/{copyFromWishListId}`
- `/api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}`



---

## Requisitions

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/requisitions`](#get-api-v1-requisitions)
- [`GET /api/v1/requisitions/{requisitionId}`](#get-api-v1-requisitions-requisitionid)
- [`GET /api/v1/requisitions/{RequisitionId}/requisitionlines`](#get-api-v1-requisitions-requisitionid-requisitionlines)
- [`GET /api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}`](#get-api-v1-requisitions-requisitionid-requisitionlines-requisitionlineid)
- [`DELETE /api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}`](#delete-api-v1-requisitions-requisitionid-requisitionlines-requisitionlineid)
- [`PATCH /api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}`](#patch-api-v1-requisitions-requisitionid-requisitionlines-requisitionlineid)

---

### `GET` /api/v1/requisitions

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.currentPage` | integer (int32) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.recalculatePrice` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RequisitionCollectionModel` |

##### Response Schema: `RequisitionCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `requisitions` | RequisitionModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/requisitions/{requisitionId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `requisitionId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RequisitionModel` |

##### Response Schema: `RequisitionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `requisitionLinesUri` | string |  |
| `isApproved` | boolean |  |
| `requisitionLineCollection` | RequisitionLineCollectionModel |  |
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

### `GET` /api/v1/requisitions/{RequisitionId}/requisitionlines

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `RequisitionId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.requisitionId` | string (uuid) | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RequisitionLineCollectionModel` |

##### Response Schema: `RequisitionLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `requisitionLines` | RequisitionLineModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `requisitionId` | string | ✅ |  |
| `requisitionLineId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RequisitionLineModel` |

##### Response Schema: `RequisitionLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `costCode` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `userName` | string |  |
| `orderDate` | string | date-time |
| `qtyOrdered` | number | decimal |
| `brand` | BrandDto |  |
| `properties` | object |  |

---

### `DELETE` /api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `requisitionId` | string | ✅ |  |
| `requisitionLineId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RequisitionModel` |

##### Response Schema: `RequisitionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `requisitionLinesUri` | string |  |
| `isApproved` | boolean |  |
| `requisitionLineCollection` | RequisitionLineCollectionModel |  |
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

### `PATCH` /api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}

**Auth required:** ✅ Yes ()

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `requisitionId` | string | ✅ |  |
| `requisitionLineId` | string | ✅ |  |

#### Request Body

**Schema:** `RequisitionLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `costCode` | string |  |
| `firstName` | string |  |
| `lastName` | string |  |
| `userName` | string |  |
| `orderDate` | string | date-time |
| `qtyOrdered` | number | decimal |
| `brand` | BrandDto |  |
| `properties` | object |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `RequisitionModel` |

##### Response Schema: `RequisitionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `requisitionLinesUri` | string |  |
| `isApproved` | boolean |  |
| `requisitionLineCollection` | RequisitionLineCollectionModel |  |
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
| `/api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}` | GET, DELETE, PATCH |

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/requisitions`
- `/api/v1/requisitions/{requisitionId}`

**Child / sub-resources:**

- `/api/v1/requisitions/{RequisitionId}/requisitionlines`
- `/api/v1/requisitions/{requisitionId}`
- `/api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{requisitionId}`

**Linked paths:**

- `/api/v1/requisitions/{requisitionId}`
- `/api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}`



---

