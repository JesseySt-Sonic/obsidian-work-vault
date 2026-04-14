---
tags:
  - storefront-api
---

# Catalogue & Discovery

Owns the product entity, category tree, and brand navigation. Price and availability endpoints are thin proxies delegating to the Pricing & Inventory service at runtime.

---

## Contents

- [[#Products]]
- [[#Categories]]
- [[#Brands]]
- [[#Brandalphabet]]
- [[#Catalogpages]]

---

## Products

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/products`](#get-api-v1-products)
- [`GET /api/v1/products/{productId}`](#get-api-v1-products-productid)
- [`GET /api/v1/products/{productId}/crosssells`](#get-api-v1-products-productid-crosssells)
- [`GET /api/v1/products/{productId}/price`](#get-api-v1-products-productid-price)
- [`GET /api/v1/products/{productId}/availability`](#get-api-v1-products-productid-availability)
- [`POST /api/v1/products/batchget`](#post-api-v1-products-batchget)
- [`GET /api/v1/products/feederData`](#get-api-v1-products-feederdata)

---

### `GET` /api/v1/products

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `model.query` | string | ❌ |  |
| `model.categoryId` | string (uuid) | ❌ |  |
| `model.brandIds` | string[] | ❌ |  |
| `model.productLineIds` | string[] | ❌ |  |
| `model.attributeValueIds` | string[] | ❌ |  |
| `model.priceFilters` | integer[] | ❌ |  |
| `model.minimumPrice` | number (double) | ❌ |  |
| `model.maximumPrice` | number (double) | ❌ |  |
| `model.sort` | string | ❌ |  |
| `model.page` | integer (int32) | ❌ |  |
| `model.pageSize` | integer (int32) | ❌ |  |
| `model.productIds` | string[] | ❌ |  |
| `model.names` | string[] | ❌ |  |
| `model.erpNumbers` | string[] | ❌ |  |
| `model.extendedNames` | string[] | ❌ |  |
| `model.replaceProducts` | boolean | ❌ |  |
| `model.priceParameters` | undefined[] | ❌ |  |
| `model.expand` | string | ❌ |  |
| `model.includeSuggestions` | boolean | ❌ |  |
| `model.searchWithin` | string | ❌ |  |
| `model.getAllAttributeFacets` | boolean | ❌ |  |
| `model.filter` | string | ❌ |  |
| `model.topSellersCategoryIds` | string[] | ❌ |  |
| `model.topSellersPersonaIds` | string[] | ❌ |  |
| `model.topSellersMaxResults` | integer (int32) | ❌ |  |
| `model.applyPersonalization` | boolean | ❌ |  |
| `model.includeAttributes` | string | ❌ |  |
| `model.includeAlternateInventory` | boolean | ❌ |  |
| `model.makeBrandUrls` | boolean | ❌ |  |
| `model.previouslyPurchasedProducts` | boolean | ❌ |  |
| `model.stockedItemsOnly` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ProductCollectionModel` |

##### Response Schema: `ProductCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `products` | ProductDto[] |  |
| `categoryFacets` | CategoryFacetDto[] |  |
| `attributeTypeFacets` | AttributeTypeFacetDto[] |  |
| `brandFacets` | GenericFacetDto[] |  |
| `productLineFacets` | GenericFacetDto[] |  |
| `didYouMeanSuggestions` | SuggestionDto[] |  |
| `priceRange` | PriceRangeDto |  |
| `exactMatch` | boolean |  |
| `notAllProductsFound` | boolean |  |
| `notAllProductsAllowed` | boolean |  |
| `originalQuery` | string |  |
| `correctedQuery` | string |  |
| `searchTermRedirectUrl` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/products/{productId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `productId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.productId` | string (uuid) | ❌ |  |
| `parameter.categoryId` | string (uuid) | ❌ |  |
| `parameter.replaceProducts` | boolean | ❌ |  |
| `parameter.unitOfMeasure` | string | ❌ |  |
| `parameter.qtyOrdered` | number (decimal) | ❌ |  |
| `parameter.configuration` | string[] | ❌ |  |
| `parameter.expand` | string | ❌ |  |
| `parameter.addToRecentlyViewed` | boolean | ❌ |  |
| `parameter.alsoPurchasedMaxResults` | integer (int32) | ❌ |  |
| `parameter.applyPersonalization` | boolean | ❌ |  |
| `parameter.includeAttributes` | string | ❌ |  |
| `parameter.includeAlternateInventory` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ProductModel` |

##### Response Schema: `ProductModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `product` | ProductDto |  |
| `properties` | object |  |

---

### `GET` /api/v1/products/{productId}/crosssells

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `productId` | string (uuid) | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CrossSellCollectionModel` |

##### Response Schema: `CrossSellCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `products` | ProductDto[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/products/{productId}/price

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `productId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `productPriceModel.productId` | string | ❌ |  |
| `productPriceModel.unitOfMeasure` | string | ❌ |  |
| `productPriceModel.qtyOrdered` | number (decimal) | ❌ |  |
| `productPriceModel.configuration` | string[] | ❌ |  |
| `productPriceModel.properties` | string | ❌ |  |
| `productPriceModel.isValid` | boolean | ❌ |  |
| `productPriceModel.validationMessage` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ProductPriceModel` |

##### Response Schema: `ProductPriceModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `productId` | string | uuid |
| `isOnSale` | boolean |  |
| `requiresRealTimePrice` | boolean |  |
| `quoteRequired` | boolean |  |
| `additionalResults` | object |  |
| `unitCost` | number | decimal |
| `unitCostDisplay` | string |  |
| `unitListPrice` | number | decimal |
| `unitListPriceDisplay` | string |  |
| `extendedUnitListPrice` | number | decimal |
| `extendedUnitListPriceDisplay` | string |  |
| `unitRegularPrice` | number | decimal |
| `unitRegularPriceDisplay` | string |  |
| `extendedUnitRegularPrice` | number | decimal |
| `extendedUnitRegularPriceDisplay` | string |  |
| `unitNetPrice` | number | decimal |
| `unitNetPriceDisplay` | string |  |
| `extendedUnitNetPrice` | number | decimal |
| `extendedUnitNetPriceDisplay` | string |  |
| `unitOfMeasure` | string |  |
| `vatRate` | number | decimal |
| `vatAmount` | number | decimal |
| `vatAmountDisplay` | string |  |
| `unitListBreakPrices` | BreakPriceDto[] |  |
| `unitRegularBreakPrices` | BreakPriceDto[] |  |
| `regularPrice` | number | decimal |
| `regularPriceDisplay` | string |  |
| `extendedRegularPrice` | number | decimal |
| `extendedRegularPriceDisplay` | string |  |
| `actualPrice` | number | decimal |
| `actualPriceDisplay` | string |  |
| `extendedActualPrice` | number | decimal |
| `extendedActualPriceDisplay` | string |  |
| `regularBreakPrices` | BreakPriceDto[] |  |
| `actualBreakPrices` | BreakPriceDto[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/products/{productId}/availability

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `productId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `productAvailabilityParameter.productId` | string | ❌ |  |
| `productAvailabilityParameter.includeAlternateInventory` | boolean | ❌ |  |
| `productAvailabilityParameter.configuration` | string[] | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ProductPriceModel` |

##### Response Schema: `ProductPriceModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `productId` | string | uuid |
| `isOnSale` | boolean |  |
| `requiresRealTimePrice` | boolean |  |
| `quoteRequired` | boolean |  |
| `additionalResults` | object |  |
| `unitCost` | number | decimal |
| `unitCostDisplay` | string |  |
| `unitListPrice` | number | decimal |
| `unitListPriceDisplay` | string |  |
| `extendedUnitListPrice` | number | decimal |
| `extendedUnitListPriceDisplay` | string |  |
| `unitRegularPrice` | number | decimal |
| `unitRegularPriceDisplay` | string |  |
| `extendedUnitRegularPrice` | number | decimal |
| `extendedUnitRegularPriceDisplay` | string |  |
| `unitNetPrice` | number | decimal |
| `unitNetPriceDisplay` | string |  |
| `extendedUnitNetPrice` | number | decimal |
| `extendedUnitNetPriceDisplay` | string |  |
| `unitOfMeasure` | string |  |
| `vatRate` | number | decimal |
| `vatAmount` | number | decimal |
| `vatAmountDisplay` | string |  |
| `unitListBreakPrices` | BreakPriceDto[] |  |
| `unitRegularBreakPrices` | BreakPriceDto[] |  |
| `regularPrice` | number | decimal |
| `regularPriceDisplay` | string |  |
| `extendedRegularPrice` | number | decimal |
| `extendedRegularPriceDisplay` | string |  |
| `actualPrice` | number | decimal |
| `actualPriceDisplay` | string |  |
| `extendedActualPrice` | number | decimal |
| `extendedActualPriceDisplay` | string |  |
| `regularBreakPrices` | BreakPriceDto[] |  |
| `actualBreakPrices` | BreakPriceDto[] |  |
| `properties` | object |  |

---

### `POST` /api/v1/products/batchget

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `BatchGetProductParameter`

| Property | Type | Description |
|----------|------|-------------|
| `extendedNames` | string[] |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ProductDto[]` |

##### Response Schema: `ProductDto[]`

| Property | Type | Description |
|----------|------|-------------|
| `id` | string | uuid |
| `orderLineId` | string | uuid |
| `name` | string |  |
| `customerName` | string |  |
| `shortDescription` | string |  |
| `erpNumber` | string |  |
| `erpDescription` | string |  |
| `urlSegment` | string |  |
| `basicListPrice` | number | decimal |
| `basicSalePrice` | number | decimal |
| `basicSaleStartDate` | string | date-time |
| `basicSaleEndDate` | string | date-time |
| `smallImagePath` | string |  |
| `mediumImagePath` | string |  |
| `largeImagePath` | string |  |
| `pricing` | ProductPriceDto |  |
| `currencySymbol` | string |  |
| `qtyOnHand` | number | decimal |
| `isConfigured` | boolean |  |
| `isFixedConfiguration` | boolean |  |
| `isActive` | boolean |  |
| `isHazardousGood` | boolean |  |
| `isDiscontinued` | boolean |  |
| `isSpecialOrder` | boolean |  |
| `isGiftCard` | boolean |  |
| `isBeingCompared` | boolean |  |
| `isSponsored` | boolean |  |
| `isSubscription` | boolean |  |
| `quoteRequired` | boolean |  |
| `manufacturerItem` | string |  |
| `packDescription` | string |  |
| `altText` | string |  |
| `customerUnitOfMeasure` | string |  |
| `canBackOrder` | boolean |  |
| `trackInventory` | boolean |  |
| `multipleSaleQty` | integer | int32 |
| `minimumOrderQty` | integer | int32 |
| `htmlContent` | string |  |
| `productCode` | string |  |
| `priceCode` | string |  |
| `sku` | string |  |
| `upcCode` | string |  |
| `modelNumber` | string |  |
| `taxCode1` | string |  |
| `taxCode2` | string |  |
| `taxCategory` | string |  |
| `shippingClassification` | string |  |
| `shippingLength` | string |  |
| `shippingWidth` | string |  |
| `shippingHeight` | string |  |
| `shippingWeight` | string |  |
| `qtyPerShippingPackage` | number | decimal |
| `shippingAmountOverride` | number | double |
| `handlingAmountOverride` | number | double |
| `metaDescription` | string |  |
| `metaKeywords` | string |  |
| `pageTitle` | string |  |
| `allowAnyGiftCardAmount` | boolean |  |
| `sortOrder` | integer | int32 |
| `hasMsds` | boolean |  |
| `unspsc` | string |  |
| `roundingRule` | string |  |
| `vendorNumber` | string |  |
| `configurationDto` | LegacyConfigurationDto |  |
| `unitOfMeasure` | string |  |
| `unitOfMeasureDisplay` | string |  |
| `unitOfMeasureDescription` | string |  |
| `selectedUnitOfMeasure` | string |  |
| `selectedUnitOfMeasureDisplay` | string |  |
| `productDetailUrl` | string |  |
| `canAddToCart` | boolean |  |
| `allowedAddToCart` | boolean |  |
| `canAddToWishlist` | boolean |  |
| `canViewDetails` | boolean |  |
| `canShowPrice` | boolean |  |
| `canShowUnitOfMeasure` | boolean |  |
| `canEnterQuantity` | boolean |  |
| `canConfigure` | boolean |  |
| `isStyleProductParent` | boolean |  |
| `styleParentId` | string | uuid |
| `requiresRealTimeInventory` | boolean |  |
| `numberInCart` | number | decimal |
| `qtyOrdered` | number | decimal |
| `availability` | AvailabilityDto |  |
| `styleTraits` | StyleTraitDto[] |  |
| `styledProducts` | StyledProductDto[] |  |
| `attributeTypes` | AttributeTypeDto[] |  |
| `documents` | DocumentDto[] |  |
| `specifications` | SpecificationDto[] |  |
| `crossSells` | ProductDto[] |  |
| `accessories` | ProductDto[] |  |
| `productUnitOfMeasures` | ProductUnitOfMeasureDto[] |  |
| `productImages` | ProductImageDto[] |  |
| `properties` | object |  |
| `score` | number | double |
| `scoreExplanation` | ScoreExplanationDto |  |
| `searchBoost` | integer | int32 |
| `searchBoostDecimal` | number | decimal |
| `salePriceLabel` | string |  |
| `cantBuy` | boolean |  |
| `allowZeroPricing` | boolean |  |
| `brand` | BrandDto |  |
| `productLine` | ProductLineDto |  |
| `productSubscription` | ProductSubscriptionDto |  |
| `replacementProductId` | string | uuid |
| `warehouses` | WarehouseDto[] |  |
| `relatedProducts` | RelatedProductDto[] |  |
| `alsoPurchasedProducts` | ProductDto[] |  |
| `openGraphTitle` | string |  |
| `openGraphUrl` | string |  |
| `openGraphImage` | string |  |
| `badges` | BadgeDto[] |  |
| `replacementProduct` | ProductDto |  |

---

### `GET` /api/v1/products/feederData

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

- `/api/v1/products`
- `/api/v1/products/{productId}`

**Child / sub-resources:**

- `/api/v1/products/batchget`
- `/api/v1/products/feederData`
- `/api/v1/products/{productId}`
- `/api/v1/products/{productId}/availability`
- `/api/v1/products/{productId}/crosssells`
- `/api/v1/products/{productId}/price`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{productId}`

**Linked paths:**

- `/api/v1/products/{productId}`
- `/api/v1/products/{productId}/availability`
- `/api/v1/products/{productId}/crosssells`
- `/api/v1/products/{productId}/price`

#### Shared Models

These response/request models are also used by other API sections:

| Model | Also used in |
|-------|--------------|
| `ProductCollectionModel` | Brands |
| `CrossSellCollectionModel` | Websites |



---

## Categories

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/categories`](#get-api-v1-categories)
- [`GET /api/v1/categories/{categoryId}`](#get-api-v1-categories-categoryid)
- [`GET /api/v1/categories/feederData`](#get-api-v1-categories-feederdata)

---

### `GET` /api/v1/categories

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.maxDepth` | integer (int32) | ❌ |  |
| `parameter.startCategoryId` | string (uuid) | ❌ |  |
| `parameter.includeStartCategory` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CategoryCollectionModel` |

##### Response Schema: `CategoryCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `categories` | CategoryModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/categories/{categoryId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `categoryId` | string (uuid) | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CategoryModel` |

##### Response Schema: `CategoryModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `parentId` | string | uuid |
| `name` | string |  |
| `shortDescription` | string |  |
| `urlSegment` | string |  |
| `smallImagePath` | string |  |
| `largeImagePath` | string |  |
| `imageAltText` | string |  |
| `activateOn` | string | date-time |
| `deactivateOn` | string | date-time |
| `metaKeywords` | string |  |
| `metaDescription` | string |  |
| `htmlContent` | string |  |
| `sortOrder` | integer | int32 |
| `isFeatured` | boolean |  |
| `isDynamic` | boolean |  |
| `subCategories` | CategoryModel[] |  |
| `path` | string |  |
| `mobileBannerImageUrl` | string |  |
| `mobilePrimaryText` | string |  |
| `mobileSecondaryText` | string |  |
| `mobileTextJustification` | string |  |
| `mobileTextColor` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/categories/feederData

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `type` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/categories`

**Child / sub-resources:**

- `/api/v1/categories/feederData`
- `/api/v1/categories/{categoryId}`



---

## Brands

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/brands/{BrandId}/categories`](#get-api-v1-brands-brandid-categories)
- [`GET /api/v1/brands/{BrandId}/categories/{CategoryId}`](#get-api-v1-brands-brandid-categories-categoryid)
- [`GET /api/v1/brands/{BrandId}/productlines/{ProductLineId}/products`](#get-api-v1-brands-brandid-productlines-productlineid-products)
- [`GET /api/v1/brands/{brandId}/products`](#get-api-v1-brands-brandid-products)
- [`GET /api/v1/brands/{BrandId}/categories/{CategoryId}/products`](#get-api-v1-brands-brandid-categories-categoryid-products)
- [`GET /api/v1/brands`](#get-api-v1-brands)
- [`GET /api/v1/brands/{BrandId}`](#get-api-v1-brands-brandid)
- [`GET /api/v1/brands/getByPath`](#get-api-v1-brands-getbypath)
- [`GET /api/v1/brands/feederData`](#get-api-v1-brands-feederdata)
- [`GET /api/v1/brands/{BrandId}/productlines`](#get-api-v1-brands-brandid-productlines)
- [`GET /api/v1/brands/{BrandId}/productlines/{ProductLineId}`](#get-api-v1-brands-brandid-productlines-productlineid)

---

### `GET` /api/v1/brands/{BrandId}/categories

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `BrandId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.brandId` | string (uuid) | ❌ |  |
| `parameter.categoryId` | string (uuid) | ❌ |  |
| `parameter.maximumDepth` | integer (int32) | ❌ |  |
| `parameter.expand` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BrandCategoryCollectionModel` |

##### Response Schema: `BrandCategoryCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `brandCategories` | BrandCategoryModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/brands/{BrandId}/categories/{CategoryId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `BrandId` | string | ✅ |  |
| `CategoryId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.brandId` | string (uuid) | ❌ |  |
| `parameter.categoryId` | string (uuid) | ❌ |  |
| `parameter.expand` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BrandCategoryModel` |

##### Response Schema: `BrandCategoryModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `brandId` | string | uuid |
| `categoryId` | string | uuid |
| `contentManagerId` | string | uuid |
| `categoryName` | string |  |
| `categoryShortDescription` | string |  |
| `featuredImagePath` | string |  |
| `featuredImageAltText` | string |  |
| `productListPagePath` | string |  |
| `htmlContent` | string |  |
| `subCategories` | BrandCategoryModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/brands/{BrandId}/productlines/{ProductLineId}/products

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `BrandId` | string | ✅ |  |
| `ProductLineId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.brandId` | string (uuid) | ❌ |  |
| `parameter.productLineId` | string (uuid) | ❌ |  |
| `parameter.query` | string | ❌ |  |
| `parameter.categoryId` | string (uuid) | ❌ |  |
| `parameter.brandIds` | string[] | ❌ |  |
| `parameter.productLineIds` | string[] | ❌ |  |
| `parameter.attributeValueIds` | string[] | ❌ |  |
| `parameter.priceFilters` | integer[] | ❌ |  |
| `parameter.minimumPrice` | number (double) | ❌ |  |
| `parameter.maximumPrice` | number (double) | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.productIds` | string[] | ❌ |  |
| `parameter.names` | string[] | ❌ |  |
| `parameter.erpNumbers` | string[] | ❌ |  |
| `parameter.extendedNames` | string[] | ❌ |  |
| `parameter.replaceProducts` | boolean | ❌ |  |
| `parameter.priceParameters` | undefined[] | ❌ |  |
| `parameter.expand` | string | ❌ |  |
| `parameter.includeSuggestions` | boolean | ❌ |  |
| `parameter.searchWithin` | string | ❌ |  |
| `parameter.getAllAttributeFacets` | boolean | ❌ |  |
| `parameter.filter` | string | ❌ |  |
| `parameter.topSellersCategoryIds` | string[] | ❌ |  |
| `parameter.topSellersPersonaIds` | string[] | ❌ |  |
| `parameter.topSellersMaxResults` | integer (int32) | ❌ |  |
| `parameter.applyPersonalization` | boolean | ❌ |  |
| `parameter.includeAttributes` | string | ❌ |  |
| `parameter.includeAlternateInventory` | boolean | ❌ |  |
| `parameter.makeBrandUrls` | boolean | ❌ |  |
| `parameter.previouslyPurchasedProducts` | boolean | ❌ |  |
| `parameter.stockedItemsOnly` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ProductCollectionModel` |

##### Response Schema: `ProductCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `products` | ProductDto[] |  |
| `categoryFacets` | CategoryFacetDto[] |  |
| `attributeTypeFacets` | AttributeTypeFacetDto[] |  |
| `brandFacets` | GenericFacetDto[] |  |
| `productLineFacets` | GenericFacetDto[] |  |
| `didYouMeanSuggestions` | SuggestionDto[] |  |
| `priceRange` | PriceRangeDto |  |
| `exactMatch` | boolean |  |
| `notAllProductsFound` | boolean |  |
| `notAllProductsAllowed` | boolean |  |
| `originalQuery` | string |  |
| `correctedQuery` | string |  |
| `searchTermRedirectUrl` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/brands/{brandId}/products

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `brandId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.brandId` | string (uuid) | ❌ |  |
| `parameter.query` | string | ❌ |  |
| `parameter.categoryId` | string (uuid) | ❌ |  |
| `parameter.brandIds` | string[] | ❌ |  |
| `parameter.productLineIds` | string[] | ❌ |  |
| `parameter.attributeValueIds` | string[] | ❌ |  |
| `parameter.priceFilters` | integer[] | ❌ |  |
| `parameter.minimumPrice` | number (double) | ❌ |  |
| `parameter.maximumPrice` | number (double) | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.productIds` | string[] | ❌ |  |
| `parameter.names` | string[] | ❌ |  |
| `parameter.erpNumbers` | string[] | ❌ |  |
| `parameter.extendedNames` | string[] | ❌ |  |
| `parameter.replaceProducts` | boolean | ❌ |  |
| `parameter.priceParameters` | undefined[] | ❌ |  |
| `parameter.expand` | string | ❌ |  |
| `parameter.includeSuggestions` | boolean | ❌ |  |
| `parameter.searchWithin` | string | ❌ |  |
| `parameter.getAllAttributeFacets` | boolean | ❌ |  |
| `parameter.filter` | string | ❌ |  |
| `parameter.topSellersCategoryIds` | string[] | ❌ |  |
| `parameter.topSellersPersonaIds` | string[] | ❌ |  |
| `parameter.topSellersMaxResults` | integer (int32) | ❌ |  |
| `parameter.applyPersonalization` | boolean | ❌ |  |
| `parameter.includeAttributes` | string | ❌ |  |
| `parameter.includeAlternateInventory` | boolean | ❌ |  |
| `parameter.makeBrandUrls` | boolean | ❌ |  |
| `parameter.previouslyPurchasedProducts` | boolean | ❌ |  |
| `parameter.stockedItemsOnly` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ProductCollectionModel` |

##### Response Schema: `ProductCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `products` | ProductDto[] |  |
| `categoryFacets` | CategoryFacetDto[] |  |
| `attributeTypeFacets` | AttributeTypeFacetDto[] |  |
| `brandFacets` | GenericFacetDto[] |  |
| `productLineFacets` | GenericFacetDto[] |  |
| `didYouMeanSuggestions` | SuggestionDto[] |  |
| `priceRange` | PriceRangeDto |  |
| `exactMatch` | boolean |  |
| `notAllProductsFound` | boolean |  |
| `notAllProductsAllowed` | boolean |  |
| `originalQuery` | string |  |
| `correctedQuery` | string |  |
| `searchTermRedirectUrl` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/brands/{BrandId}/categories/{CategoryId}/products

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `BrandId` | string | ✅ |  |
| `CategoryId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.brandId` | string (uuid) | ❌ |  |
| `parameter.query` | string | ❌ |  |
| `parameter.categoryId` | string (uuid) | ❌ |  |
| `parameter.brandIds` | string[] | ❌ |  |
| `parameter.productLineIds` | string[] | ❌ |  |
| `parameter.attributeValueIds` | string[] | ❌ |  |
| `parameter.priceFilters` | integer[] | ❌ |  |
| `parameter.minimumPrice` | number (double) | ❌ |  |
| `parameter.maximumPrice` | number (double) | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.productIds` | string[] | ❌ |  |
| `parameter.names` | string[] | ❌ |  |
| `parameter.erpNumbers` | string[] | ❌ |  |
| `parameter.extendedNames` | string[] | ❌ |  |
| `parameter.replaceProducts` | boolean | ❌ |  |
| `parameter.priceParameters` | undefined[] | ❌ |  |
| `parameter.expand` | string | ❌ |  |
| `parameter.includeSuggestions` | boolean | ❌ |  |
| `parameter.searchWithin` | string | ❌ |  |
| `parameter.getAllAttributeFacets` | boolean | ❌ |  |
| `parameter.filter` | string | ❌ |  |
| `parameter.topSellersCategoryIds` | string[] | ❌ |  |
| `parameter.topSellersPersonaIds` | string[] | ❌ |  |
| `parameter.topSellersMaxResults` | integer (int32) | ❌ |  |
| `parameter.applyPersonalization` | boolean | ❌ |  |
| `parameter.includeAttributes` | string | ❌ |  |
| `parameter.includeAlternateInventory` | boolean | ❌ |  |
| `parameter.makeBrandUrls` | boolean | ❌ |  |
| `parameter.previouslyPurchasedProducts` | boolean | ❌ |  |
| `parameter.stockedItemsOnly` | boolean | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ProductCollectionModel` |

##### Response Schema: `ProductCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `products` | ProductDto[] |  |
| `categoryFacets` | CategoryFacetDto[] |  |
| `attributeTypeFacets` | AttributeTypeFacetDto[] |  |
| `brandFacets` | GenericFacetDto[] |  |
| `productLineFacets` | GenericFacetDto[] |  |
| `didYouMeanSuggestions` | SuggestionDto[] |  |
| `priceRange` | PriceRangeDto |  |
| `exactMatch` | boolean |  |
| `notAllProductsFound` | boolean |  |
| `notAllProductsAllowed` | boolean |  |
| `originalQuery` | string |  |
| `correctedQuery` | string |  |
| `searchTermRedirectUrl` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/brands

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.startsWith` | string | ❌ |  |
| `parameter.manufacturer` | string | ❌ |  |
| `parameter.expand` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |
| `parameter.randomize` | boolean | ❌ |  |
| `parameter.brandIds` | string[] | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BrandCollectionModel` |

##### Response Schema: `BrandCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `brands` | BrandModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/brands/{BrandId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `BrandId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.brandId` | string (uuid) | ❌ |  |
| `parameter.expand` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BrandModel` |

##### Response Schema: `BrandModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `manufacturer` | string |  |
| `externalUrl` | string |  |
| `detailPagePath` | string |  |
| `productListPagePath` | string |  |
| `logoSmallImagePath` | string |  |
| `logoLargeImagePath` | string |  |
| `logoAltText` | string |  |
| `featuredImagePath` | string |  |
| `featuredImageAltText` | string |  |
| `topSellerProducts` | ProductDto[] |  |
| `alternateLanguageUrls` | object |  |
| `htmlContent` | string |  |
| `pageTitle` | string |  |
| `metaDescription` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/brands/getByPath

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `path` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BrandModel` |

##### Response Schema: `BrandModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `manufacturer` | string |  |
| `externalUrl` | string |  |
| `detailPagePath` | string |  |
| `productListPagePath` | string |  |
| `logoSmallImagePath` | string |  |
| `logoLargeImagePath` | string |  |
| `logoAltText` | string |  |
| `featuredImagePath` | string |  |
| `featuredImageAltText` | string |  |
| `topSellerProducts` | ProductDto[] |  |
| `alternateLanguageUrls` | object |  |
| `htmlContent` | string |  |
| `pageTitle` | string |  |
| `metaDescription` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/brands/feederData

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/brands/{BrandId}/productlines

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `BrandId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.brandId` | string (uuid) | ❌ |  |
| `parameter.getFeatured` | boolean | ❌ |  |
| `parameter.getSponsored` | boolean | ❌ |  |
| `parameter.expand` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BrandProductLineCollectionModel` |

##### Response Schema: `BrandProductLineCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `pagination` | PaginationModel |  |
| `productLines` | BrandProductLineModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/brands/{BrandId}/productlines/{ProductLineId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `BrandId` | string | ✅ |  |
| `ProductLineId` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.brandId` | string (uuid) | ❌ |  |
| `parameter.productLineId` | string (uuid) | ❌ |  |
| `parameter.expand` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BrandProductLineModel` |

##### Response Schema: `BrandProductLineModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string | uuid |
| `name` | string |  |
| `sortOrder` | integer | int32 |
| `productListPagePath` | string |  |
| `featuredImagePath` | string |  |
| `featuredImageAltText` | string |  |
| `isFeatured` | boolean |  |
| `isSponsored` | boolean |  |
| `properties` | object |  |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/brands`
- `/api/v1/brands/{BrandId}`
- `/api/v1/brands/{BrandId}/categories`
- `/api/v1/brands/{BrandId}/categories/{CategoryId}`
- `/api/v1/brands/{BrandId}/productlines`
- `/api/v1/brands/{BrandId}/productlines/{ProductLineId}`

**Child / sub-resources:**

- `/api/v1/brands/feederData`
- `/api/v1/brands/getByPath`
- `/api/v1/brands/{BrandId}`
- `/api/v1/brands/{brandId}/products`
- `/api/v1/brands/{BrandId}/categories`
- `/api/v1/brands/{BrandId}/productlines`
- `/api/v1/brands/{BrandId}/categories/{CategoryId}`
- `/api/v1/brands/{BrandId}/categories/{CategoryId}/products`
- `/api/v1/brands/{BrandId}/productlines/{ProductLineId}`
- `/api/v1/brands/{BrandId}/productlines/{ProductLineId}/products`

#### ID-Linked Resources

These path parameters create explicit links between resources:

##### `{BrandId}`

**Linked paths:**

- `/api/v1/brands/{BrandId}`
- `/api/v1/brands/{BrandId}/categories`
- `/api/v1/brands/{BrandId}/categories/{CategoryId}`
- `/api/v1/brands/{BrandId}/categories/{CategoryId}/products`
- `/api/v1/brands/{BrandId}/productlines`
- `/api/v1/brands/{BrandId}/productlines/{ProductLineId}`
- `/api/v1/brands/{BrandId}/productlines/{ProductLineId}/products`

##### `{CategoryId}`

**Linked paths:**

- `/api/v1/brands/{BrandId}/categories/{CategoryId}`
- `/api/v1/brands/{BrandId}/categories/{CategoryId}/products`

##### `{ProductLineId}`

**Linked paths:**

- `/api/v1/brands/{BrandId}/productlines/{ProductLineId}`
- `/api/v1/brands/{BrandId}/productlines/{ProductLineId}/products`

#### Shared Models

These response/request models are also used by other API sections:

| Model | Also used in |
|-------|--------------|
| `ProductCollectionModel` | Products |



---

## Brandalphabet

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/brandalphabet`](#get-api-v1-brandalphabet)

---

### `GET` /api/v1/brandalphabet

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `BrandAlphabetModel` |

##### Response Schema: `BrandAlphabetModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `alphabet` | BrandAlphabetLetterModel[] |  |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Catalogpages

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/catalogpages`](#get-api-v1-catalogpages)

---

### `GET` /api/v1/catalogpages

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `path` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CatalogPageModel` |

##### Response Schema: `CatalogPageModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `category` | CategoryModel |  |
| `brandId` | string | uuid |
| `productLineId` | string | uuid |
| `productId` | string | uuid |
| `productName` | string |  |
| `title` | string |  |
| `metaDescription` | string |  |
| `metaKeywords` | string |  |
| `canonicalPath` | string |  |
| `alternateLanguageUrls` | object |  |
| `isReplacementProduct` | boolean |  |
| `breadCrumbs` | BreadCrumbModel[] |  |
| `obsoletePath` | boolean |  |
| `needRedirect` | boolean |  |
| `redirectUrl` | string |  |
| `primaryImagePath` | string |  |
| `openGraphTitle` | string |  |
| `openGraphImage` | string |  |
| `openGraphUrl` | string |  |
| `structuredPageData` | string |  |
| `enableStructuredPageData` | boolean |  |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

