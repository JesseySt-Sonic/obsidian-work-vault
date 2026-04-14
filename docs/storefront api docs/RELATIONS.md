---
tags:
  - storefront-api
---

# Storefront API V1 — Endpoint Relationships

This document maps how endpoints relate to each other across the API.

---

## Resource Hierarchy

Indented paths indicate parent → child sub-resource relationships.

```
/api/v1/accounts  [GET, POST]
  /api/v1/accounts/current/paymentprofiles  [GET, POST]
    /api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}  [GET, DELETE, PATCH]
  /api/v1/accounts/vmi/import  [POST]
  /api/v1/accounts/vmi/{vmiUserId}  [PATCH]
  /api/v1/accounts/{accountId}  [GET, PATCH]
    /api/v1/accounts/{accountId}/shiptos  [PATCH]
/api/v1/adyen/config  [GET]
/api/v1/algolia/export/category  [GET]
/api/v1/algolia/export/categorystructured  [GET]
/api/v1/algolia/export/product  [GET]
/api/v1/algolia/export/restriction  [GET]
/api/v1/autocomplete  [GET]
  /api/v1/autocomplete/products  [GET]
/api/v1/bff/{path}  [GET, PUT, POST, DELETE, PATCH]
/api/v1/billtos  [GET, POST]
  /api/v1/billtos/{billToId}  [GET, PATCH]
    /api/v1/billtos/{billToId}/shiptos  [GET, POST]
      /api/v1/billtos/{billToId}/shiptos/{shipToId}  [GET, PATCH]
/api/v1/brandalphabet  [GET]
/api/v1/brands  [GET]
  /api/v1/brands/feederData  [GET]
  /api/v1/brands/getByPath  [GET]
  /api/v1/brands/{BrandId}  [GET]
    /api/v1/brands/{BrandId}/categories  [GET]
      /api/v1/brands/{BrandId}/categories/{CategoryId}  [GET]
        /api/v1/brands/{BrandId}/categories/{CategoryId}/products  [GET]
    /api/v1/brands/{BrandId}/productlines  [GET]
      /api/v1/brands/{BrandId}/productlines/{ProductLineId}  [GET]
        /api/v1/brands/{BrandId}/productlines/{ProductLineId}/products  [GET]
  /api/v1/brands/{brandId}/products  [GET]
/api/v1/budgetcalendars  [GET]
  /api/v1/budgetcalendars/{fiscalYear}  [GET, PATCH]
/api/v1/budgets  [GET]
  /api/v1/budgets/{fiscalYear}  [GET, PATCH]
/api/v1/carts  [GET, POST]
  /api/v1/carts/{cartId}  [GET, DELETE, PATCH]
    /api/v1/carts/{cartId}/cartlines  [POST, DELETE]
      /api/v1/carts/{cartId}/cartlines/batch  [POST]
      /api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}  [POST]
      /api/v1/carts/{cartId}/cartlines/{cartLineId}  [GET, DELETE, PATCH]
    /api/v1/carts/{cartId}/promotions  [GET, POST, DELETE]
      /api/v1/carts/{cartId}/promotions/{promotionId}  [GET, DELETE]
/api/v1/catalogpages  [GET]
/api/v1/categories  [GET]
  /api/v1/categories/feederData  [GET]
  /api/v1/categories/{categoryId}  [GET]
/api/v1/custom/countrylanguage  [GET]
/api/v1/custom/customer  [POST]
/api/v1/custom/finance/credit/breakdown  [GET]
/api/v1/custom/finance/credit/checkCreditLimitExceed  [POST]
/api/v1/custom/finance/credit/checkOverrideCreditBlock  [GET]
/api/v1/custom/finance/credit/overrideCreditBlock  [POST]
/api/v1/custom/messageLog/{webOrderNumber}  [GET, DELETE]
  /api/v1/custom/messageLog/{webOrderNumber}/{fileName}  [GET]
/api/v1/custom/orderhistory/{webOrderNumber}/update  [GET]
/api/v1/custom/orderprocessed  [POST]
/api/v1/custom/productprice  [POST]
/api/v1/dashboardpanels  [GET]
/api/v1/dealers  [GET]
  /api/v1/dealers/{dealerId}  [GET]
/api/v1/email  [GET]
  /api/v1/email/contactUs  [POST]
  /api/v1/email/tellafriend  [POST]
/api/v1/feederdata/brands/mostProducts  [GET]
/api/v1/feederdata/customers/mostShipTos  [GET]
/api/v1/feederdata/product/mostWarehouses  [GET]
/api/v1/feederdata/quickorder/products  [GET]
/api/v1/feederdata/restrictionGroups/mostProducts  [GET]
/api/v1/feederdata/wishLists/mostProducts  [GET]
/api/v1/invoices  [GET]
  /api/v1/invoices/shareinvoice  [POST]
  /api/v1/invoices/{invoiceId}  [GET]
/api/v1/jobquotes  [GET]
  /api/v1/jobquotes/{jobQuoteId}  [GET, PATCH]
/api/v1/locale  [POST]
/api/v1/messages  [GET, POST]
  /api/v1/messages/{messageId}  [GET, PATCH]
/api/v1/mobilecontent/{PageName}  [GET]
/api/v1/orderapprovals  [GET]
  /api/v1/orderapprovals/{cartId}  [GET]
/api/v1/orderfeed  [GET]
/api/v1/orders  [GET]
  /api/v1/orders/shareorder  [POST]
  /api/v1/orders/{orderId}  [GET, PATCH]
    /api/v1/orders/{orderId}/returns  [POST]
/api/v1/orderstatusmappings  [GET]
/api/v1/paymentauthentication  [POST]
  /api/v1/paymentauthentication/adyenpayment  [POST]
  /api/v1/paymentauthentication/adyenpaymentdetails  [POST]
  /api/v1/paymentauthentication/adyenrefund  [POST]
  /api/v1/paymentauthentication/adyenwebhook  [POST]
  /api/v1/paymentauthentication/threedscallback  [POST]
  /api/v1/paymentauthentication/threedschallengeresponse  [POST]
  /api/v1/paymentauthentication/threedsnotify  [POST]
/api/v1/paymetric/config  [POST]
/api/v1/paymetric/responsepacket  [GET]
/api/v1/products  [GET]
  /api/v1/products/batchget  [POST]
  /api/v1/products/feederData  [GET]
  /api/v1/products/{productId}  [GET]
    /api/v1/products/{productId}/availability  [GET]
    /api/v1/products/{productId}/crosssells  [GET]
    /api/v1/products/{productId}/price  [GET]
/api/v1/productsrssfeed  [GET]
/api/v1/punchout/orderrequest  [POST]
/api/v1/punchout/porequisition  [GET]
/api/v1/punchout/profiletransactionrequest  [POST]
/api/v1/punchout/sessionrequest  [GET]
/api/v1/punchout/setuprequest  [POST]
/api/v1/quotes  [GET, POST]
  /api/v1/quotes/{quoteId}  [GET, DELETE, PATCH]
    /api/v1/quotes/{quoteId}/messages  [POST]
    /api/v1/quotes/{quoteId}/quotelines/{quoteLineId}  [GET, PATCH]
/api/v1/realtimecartinventory  [POST]
/api/v1/realtimeinventory  [POST]
/api/v1/realtimepricing  [POST]
/api/v1/requisitions  [GET]
  /api/v1/requisitions/{RequisitionId}/requisitionlines  [GET]
  /api/v1/requisitions/{requisitionId}  [GET]
    /api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}  [GET, DELETE, PATCH]
/api/v1/sessions  [POST]
  /api/v1/sessions/current  [GET, DELETE, PATCH]
/api/v1/settings  [GET]
  /api/v1/settings/account  [GET]
  /api/v1/settings/cart  [GET]
  /api/v1/settings/mobileapp  [GET]
  /api/v1/settings/products  [GET]
  /api/v1/settings/quote  [GET]
  /api/v1/settings/website  [GET]
  /api/v1/settings/wishlist  [GET]
/api/v1/spreedly/config  [GET]
/api/v1/tokenexconfig  [GET]
/api/v1/translationdictionaries  [GET]
/api/v1/vmiBins/count  [GET]
/api/v1/vmiLocations  [GET, POST]
  /api/v1/vmiLocations/batch  [POST, DELETE]
  /api/v1/vmiLocations/{VmiLocationId}/notes  [GET]
  /api/v1/vmiLocations/{vmiLocationId}  [GET, DELETE, PATCH]
    /api/v1/vmiLocations/{vmiLocationId}/bins  [GET, POST]
      /api/v1/vmiLocations/{vmiLocationId}/bins/batch  [POST, DELETE]
      /api/v1/vmiLocations/{vmiLocationId}/bins/send-pdf  [POST]
      /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}  [DELETE, PATCH]
        /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts  [POST]
          /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/batch  [POST]
          /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}  [GET, DELETE, PATCH]
        /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes  [POST]
          /api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}  [DELETE, PATCH]
/api/v1/warehouses  [GET]
  /api/v1/warehouses/{warehouseId}  [GET]
/api/v1/websites/current  [GET]
  /api/v1/websites/current/addressfields  [GET]
  /api/v1/websites/current/countries  [GET]
    /api/v1/websites/current/countries/{countryId}  [GET]
  /api/v1/websites/current/crosssells  [GET]
  /api/v1/websites/current/currencies  [GET]
    /api/v1/websites/current/currencies/{currencyId}  [GET]
  /api/v1/websites/current/languages  [GET]
    /api/v1/websites/current/languages/{languageId}  [GET]
  /api/v1/websites/current/sitemessages  [GET]
  /api/v1/websites/current/states  [GET]
    /api/v1/websites/current/states/{stateId}  [GET]
/api/v1/wishlists  [GET, POST]
  /api/v1/wishlists/activateinvite  [PATCH]
  /api/v1/wishlists/{wishListId}  [GET, DELETE, PATCH]
    /api/v1/wishlists/{wishListId}/schedule  [PATCH]
    /api/v1/wishlists/{wishListId}/send-pdf  [POST]
    /api/v1/wishlists/{wishListId}/sendacopy  [PATCH]
    /api/v1/wishlists/{wishListId}/share/{wishListShareId}  [DELETE]
    /api/v1/wishlists/{wishListId}/tags/batch  [POST, DELETE]
    /api/v1/wishlists/{wishListId}/wishlistlines  [GET, POST]
      /api/v1/wishlists/{wishListId}/wishlistlines/batch  [DELETE, PATCH]
        /api/v1/wishlists/{wishListId}/wishlistlines/batch/{copyFromWishListId}  [POST]
      /api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}  [GET, DELETE, PATCH]
```

## CRUD Operation Groups

Paths that expose multiple HTTP methods (full or partial CRUD):

| Path                                                                          | Methods                       |
| ----------------------------------------------------------------------------- | ----------------------------- |
| `/api/v1/accounts`                                                            | GET, POST                     |
| `/api/v1/accounts/current/paymentprofiles`                                    | GET, POST                     |
| `/api/v1/accounts/current/paymentprofiles/{AccountPaymentProfileId}`          | GET, DELETE, PATCH            |
| `/api/v1/accounts/{accountId}`                                                | GET, PATCH                    |
| `/api/v1/bff/{path}`                                                          | GET, PUT, POST, DELETE, PATCH |
| `/api/v1/billtos`                                                             | GET, POST                     |
| `/api/v1/billtos/{billToId}`                                                  | GET, PATCH                    |
| `/api/v1/billtos/{billToId}/shiptos`                                          | GET, POST                     |
| `/api/v1/billtos/{billToId}/shiptos/{shipToId}`                               | GET, PATCH                    |
| `/api/v1/budgetcalendars/{fiscalYear}`                                        | GET, PATCH                    |
| `/api/v1/budgets/{fiscalYear}`                                                | GET, PATCH                    |
| `/api/v1/carts`                                                               | GET, POST                     |
| `/api/v1/carts/{cartId}`                                                      | GET, DELETE, PATCH            |
| `/api/v1/carts/{cartId}/cartlines`                                            | POST, DELETE                  |
| `/api/v1/carts/{cartId}/cartlines/{cartLineId}`                               | GET, DELETE, PATCH            |
| `/api/v1/carts/{cartId}/promotions`                                           | GET, POST, DELETE             |
| `/api/v1/carts/{cartId}/promotions/{promotionId}`                             | GET, DELETE                   |
| `/api/v1/custom/messageLog/{webOrderNumber}`                                  | GET, DELETE                   |
| `/api/v1/jobquotes/{jobQuoteId}`                                              | GET, PATCH                    |
| `/api/v1/messages`                                                            | GET, POST                     |
| `/api/v1/messages/{messageId}`                                                | GET, PATCH                    |
| `/api/v1/orders/{orderId}`                                                    | GET, PATCH                    |
| `/api/v1/quotes`                                                              | GET, POST                     |
| `/api/v1/quotes/{quoteId}`                                                    | GET, DELETE, PATCH            |
| `/api/v1/quotes/{quoteId}/quotelines/{quoteLineId}`                           | GET, PATCH                    |
| `/api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}`   | GET, DELETE, PATCH            |
| `/api/v1/sessions/current`                                                    | GET, DELETE, PATCH            |
| `/api/v1/vmiLocations`                                                        | GET, POST                     |
| `/api/v1/vmiLocations/batch`                                                  | POST, DELETE                  |
| `/api/v1/vmiLocations/{vmiLocationId}`                                        | GET, DELETE, PATCH            |
| `/api/v1/vmiLocations/{vmiLocationId}/bins`                                   | GET, POST                     |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/batch`                             | POST, DELETE                  |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}`                        | DELETE, PATCH                 |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}` | GET, DELETE, PATCH            |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}`      | DELETE, PATCH                 |
| `/api/v1/wishlists`                                                           | GET, POST                     |
| `/api/v1/wishlists/{wishListId}`                                              | GET, DELETE, PATCH            |
| `/api/v1/wishlists/{wishListId}/tags/batch`                                   | POST, DELETE                  |
| `/api/v1/wishlists/{wishListId}/wishlistlines`                                | GET, POST                     |
| `/api/v1/wishlists/{wishListId}/wishlistlines/batch`                          | DELETE, PATCH                 |
| `/api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}`               | GET, DELETE, PATCH            |

## ID-Linked Resource Chains

These path parameters link resources across multiple endpoints:

### `{accountId}`

**Touches tags:** Accounts

| Path | Methods |
|------|---------|
| `/api/v1/accounts/{accountId}` | GET, PATCH |
| `/api/v1/accounts/{accountId}/shiptos` | PATCH |

### `{billToId}`

**Touches tags:** Billtos

| Path | Methods |
|------|---------|
| `/api/v1/billtos/{billToId}` | GET, PATCH |
| `/api/v1/billtos/{billToId}/shiptos` | GET, POST |
| `/api/v1/billtos/{billToId}/shiptos/{shipToId}` | GET, PATCH |

### `{BrandId}`

**Touches tags:** Brands

| Path | Methods |
|------|---------|
| `/api/v1/brands/{BrandId}` | GET |
| `/api/v1/brands/{BrandId}/categories` | GET |
| `/api/v1/brands/{BrandId}/categories/{CategoryId}` | GET |
| `/api/v1/brands/{BrandId}/categories/{CategoryId}/products` | GET |
| `/api/v1/brands/{BrandId}/productlines` | GET |
| `/api/v1/brands/{BrandId}/productlines/{ProductLineId}` | GET |
| `/api/v1/brands/{BrandId}/productlines/{ProductLineId}/products` | GET |

### `{CategoryId}`

**Touches tags:** Brands

| Path | Methods |
|------|---------|
| `/api/v1/brands/{BrandId}/categories/{CategoryId}` | GET |
| `/api/v1/brands/{BrandId}/categories/{CategoryId}/products` | GET |

### `{ProductLineId}`

**Touches tags:** Brands

| Path | Methods |
|------|---------|
| `/api/v1/brands/{BrandId}/productlines/{ProductLineId}` | GET |
| `/api/v1/brands/{BrandId}/productlines/{ProductLineId}/products` | GET |

### `{fiscalYear}`

**Touches tags:** Budgetcalendars, Budgets

| Path | Methods |
|------|---------|
| `/api/v1/budgetcalendars/{fiscalYear}` | GET, PATCH |
| `/api/v1/budgets/{fiscalYear}` | GET, PATCH |

### `{cartId}`

**Touches tags:** Carts, Orderapprovals

| Path | Methods |
|------|---------|
| `/api/v1/carts/{cartId}` | GET, DELETE, PATCH |
| `/api/v1/carts/{cartId}/cartlines` | POST, DELETE |
| `/api/v1/carts/{cartId}/cartlines/batch` | POST |
| `/api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}` | POST |
| `/api/v1/carts/{cartId}/cartlines/{cartLineId}` | GET, DELETE, PATCH |
| `/api/v1/carts/{cartId}/promotions` | GET, POST, DELETE |
| `/api/v1/carts/{cartId}/promotions/{promotionId}` | GET, DELETE |
| `/api/v1/orderapprovals/{cartId}` | GET |

### `{wishListId}`

**Touches tags:** Carts, Wishlists

| Path | Methods |
|------|---------|
| `/api/v1/carts/{cartId}/cartlines/wishlist/{wishListId}` | POST |
| `/api/v1/wishlists/{wishListId}` | GET, DELETE, PATCH |
| `/api/v1/wishlists/{wishListId}/schedule` | PATCH |
| `/api/v1/wishlists/{wishListId}/send-pdf` | POST |
| `/api/v1/wishlists/{wishListId}/sendacopy` | PATCH |
| `/api/v1/wishlists/{wishListId}/share/{wishListShareId}` | DELETE |
| `/api/v1/wishlists/{wishListId}/tags/batch` | POST, DELETE |
| `/api/v1/wishlists/{wishListId}/wishlistlines` | GET, POST |
| `/api/v1/wishlists/{wishListId}/wishlistlines/batch` | DELETE, PATCH |
| `/api/v1/wishlists/{wishListId}/wishlistlines/batch/{copyFromWishListId}` | POST |
| `/api/v1/wishlists/{wishListId}/wishlistlines/{wishListLineId}` | GET, DELETE, PATCH |

### `{webOrderNumber}`

**Touches tags:** Custom

| Path | Methods |
|------|---------|
| `/api/v1/custom/messageLog/{webOrderNumber}` | GET, DELETE |
| `/api/v1/custom/messageLog/{webOrderNumber}/{fileName}` | GET |
| `/api/v1/custom/orderhistory/{webOrderNumber}/update` | GET |

### `{orderId}`

**Touches tags:** Orders

| Path | Methods |
|------|---------|
| `/api/v1/orders/{orderId}` | GET, PATCH |
| `/api/v1/orders/{orderId}/returns` | POST |

### `{productId}`

**Touches tags:** Products

| Path | Methods |
|------|---------|
| `/api/v1/products/{productId}` | GET |
| `/api/v1/products/{productId}/availability` | GET |
| `/api/v1/products/{productId}/crosssells` | GET |
| `/api/v1/products/{productId}/price` | GET |

### `{quoteId}`

**Touches tags:** Quotes

| Path | Methods |
|------|---------|
| `/api/v1/quotes/{quoteId}` | GET, DELETE, PATCH |
| `/api/v1/quotes/{quoteId}/messages` | POST |
| `/api/v1/quotes/{quoteId}/quotelines/{quoteLineId}` | GET, PATCH |

### `{requisitionId}`

**Touches tags:** Requisitions

| Path | Methods |
|------|---------|
| `/api/v1/requisitions/{requisitionId}` | GET |
| `/api/v1/requisitions/{requisitionId}/requisitionlines/{requisitionLineId}` | GET, DELETE, PATCH |

### `{vmiLocationId}`

**Touches tags:** VmiLocations

| Path | Methods |
|------|---------|
| `/api/v1/vmiLocations/{vmiLocationId}` | GET, DELETE, PATCH |
| `/api/v1/vmiLocations/{vmiLocationId}/bins` | GET, POST |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/batch` | POST, DELETE |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/send-pdf` | POST |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}` | DELETE, PATCH |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts` | POST |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/batch` | POST |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}` | GET, DELETE, PATCH |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes` | POST |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}` | DELETE, PATCH |

### `{vmiBinId}`

**Touches tags:** VmiLocations

| Path | Methods |
|------|---------|
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}` | DELETE, PATCH |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts` | POST |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/batch` | POST |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/binCounts/{vmiCountId}` | GET, DELETE, PATCH |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes` | POST |
| `/api/v1/vmiLocations/{vmiLocationId}/bins/{vmiBinId}/notes/{vmiNoteId}` | DELETE, PATCH |

## Cross-Tag Shared Models

These models are referenced by endpoints in multiple API sections:

| Model | Used in |
|-------|---------|
| `ProductCollectionModel` | Brands, Products |
| `CartModel` | Carts, Orderapprovals |
| `ShareEntityModel` | Invoices, Orders |
| `CrossSellCollectionModel` | Products, Websites |

