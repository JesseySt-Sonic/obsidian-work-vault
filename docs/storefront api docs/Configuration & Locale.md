---
tags:
  - storefront-api
---

# Configuration & Locale

Site-wide settings, locale and language data, website metadata, translation dictionaries, and CMS content. Loaded as a bootstrap dependency before any user-facing feature.

---

## Contents

- [[#Settings]]
- [[#Websites]]
- [[#Locale]]
- [[#Translationdictionaries]]
- [[#Dashboardpanels]]
- [[#Mobilecontent]]

---

## Settings

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/settings/website`](#get-api-v1-settings-website)
- [`GET /api/v1/settings/quote`](#get-api-v1-settings-quote)
- [`GET /api/v1/settings/cart`](#get-api-v1-settings-cart)
- [`GET /api/v1/settings/account`](#get-api-v1-settings-account)
- [`GET /api/v1/settings/wishlist`](#get-api-v1-settings-wishlist)
- [`GET /api/v1/settings`](#get-api-v1-settings)
- [`GET /api/v1/settings/products`](#get-api-v1-settings-products)
- [`GET /api/v1/settings/mobileapp`](#get-api-v1-settings-mobileapp)

---

### `GET` /api/v1/settings/website

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WebsiteSettingsModel` |

##### Response Schema: `WebsiteSettingsModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `mobileAppEnabled` | boolean |  |
| `useTokenExGateway` | boolean |  |
| `useECheckTokenExGateway` | boolean |  |
| `tokenExTestMode` | boolean |  |
| `usePaymetricGateway` | boolean |  |
| `useAdyenDropIn` | boolean |  |
| `useSpreedlyDropIn` | boolean |  |
| `paymentGatewayRequiresAuthentication` | boolean |  |
| `defaultPageSize` | integer | int32 |
| `enableCookiePrivacyPolicyPopup` | boolean |  |
| `enableDynamicRecommendations` | boolean |  |
| `disableGoogleScriptsInclusion` | boolean |  |
| `googleMapsApiKey` | string |  |
| `googleTrackingTypeComputed` | string |  |
| `googleTrackingAccountId` | string |  |
| `cmsType` | integer | int32 |
| `includeSiteNameInPageTitle` | boolean |  |
| `pageTitleDelimiter` | string |  |
| `siteNameAfterTitle` | boolean |  |
| `reCaptchaSiteKey` | string |  |
| `reCaptchaEnabledForContactUs` | boolean |  |
| `reCaptchaEnabledForCreateAccount` | boolean |  |
| `reCaptchaEnabledForForgotPassword` | boolean |  |
| `reCaptchaEnabledForShareProduct` | boolean |  |
| `reCaptchaEnabledForOrderStatus` | boolean |  |
| `advancedSpireCmsFeatures` | boolean |  |
| `previewLoginEnabled` | boolean |  |
| `maintenanceModeEnabled` | boolean |  |
| `useSquareGateway` | boolean |  |
| `squareApplicationId` | string |  |
| `squareLocationId` | string |  |
| `squareLive` | boolean |  |
| `enableTokenAuthentication` | boolean |  |
| `includeRealTimeInventoryAndPricingForSeo` | boolean |  |
| `contentPagesMetadataGeneration` | boolean |  |
| `allowSocialPostGeneration` | boolean |  |
| `enableProductStructuredData` | boolean |  |
| `enableOrganizationStructuredData` | boolean |  |
| `usePaystandDropIn` | boolean |  |
| `paystandPublishableKey` | string |  |
| `paystandTestMode` | boolean |  |
| `enableCdnPrefix` | boolean |  |
| `cdnPrefix` | string |  |
| `enableBreadcrumbStructuredData` | boolean |  |
| `enableSitelinksSearchBoxStructuredData` | boolean |  |
| `enableOdpTracking` | boolean |  |
| `enableOdpStorefrontEvents` | boolean |  |
| `enableOdpTrackingAtCustomerShipToLevel` | boolean |  |
| `odpJsTagUrl` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/settings/quote

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `QuoteSettingsModel` |

##### Response Schema: `QuoteSettingsModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `jobQuoteEnabled` | boolean |  |
| `quoteExpireDays` | integer | int32 |
| `properties` | object |  |

---

### `GET` /api/v1/settings/cart

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CartSettingsModel` |

##### Response Schema: `CartSettingsModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `canRequestDeliveryDate` | boolean |  |
| `canRequisition` | boolean |  |
| `canEditCostCode` | boolean |  |
| `maximumDeliveryPeriod` | integer | int32 |
| `showCostCode` | boolean |  |
| `showPoNumber` | boolean |  |
| `showPayPal` | boolean |  |
| `showCreditCard` | boolean |  |
| `showTaxAndShipping` | boolean |  |
| `showLineNotes` | boolean |  |
| `showNewsletterSignup` | boolean |  |
| `requiresPoNumber` | boolean |  |
| `addToCartPopupTimeout` | integer | int32 |
| `enableRequestPickUpDate` | boolean |  |
| `enableSavedCreditCards` | boolean |  |
| `bypassCvvForSavedCards` | boolean |  |
| `onePageCheckout` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/settings/account

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AccountSettingsModel` |

##### Response Schema: `AccountSettingsModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `allowCreateAccount` | boolean |  |
| `allowGuestCheckout` | boolean |  |
| `allowSubscribeToNewsLetter` | boolean |  |
| `allowEmptyShipping` | boolean |  |
| `requireSelectCustomerOnSignIn` | boolean |  |
| `passwordMinimumLength` | integer | int32 |
| `passwordMinimumRequiredLength` | integer | int32 |
| `passwordRequiresSpecialCharacter` | boolean |  |
| `passwordRequiresUppercase` | boolean |  |
| `passwordRequiresLowercase` | boolean |  |
| `passwordRequiresDigit` | boolean |  |
| `rememberMe` | boolean |  |
| `keepMeSignedIn` | boolean |  |
| `daysToRetainUser` | integer | int32 |
| `useEmailAsUserName` | boolean |  |
| `enableWarehousePickup` | boolean |  |
| `logOutUserAfterPasswordChange` | boolean |  |
| `requireActivateAccount` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/settings/wishlist

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WishListSettingsModel` |

##### Response Schema: `WishListSettingsModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `allowMultipleWishLists` | boolean |  |
| `allowEditingOfWishLists` | boolean |  |
| `allowWishListsByCustomer` | boolean |  |
| `allowListSharing` | boolean |  |
| `productsPerPage` | integer | int32 |
| `enableWishListReminders` | boolean |  |
| `showAutoGeneratedLists` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/settings

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---

### `GET` /api/v1/settings/products

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `ProductSettingsModel` |

##### Response Schema: `ProductSettingsModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `allowBackOrder` | boolean |  |
| `allowBackOrderForDelivery` | boolean |  |
| `allowBackOrderForPickup` | boolean |  |
| `showInventoryAvailability` | boolean |  |
| `showAddToCartConfirmationDialog` | boolean |  |
| `enableProductComparisons` | boolean |  |
| `alternateUnitsOfMeasure` | boolean |  |
| `thirdPartyReviews` | string |  |
| `defaultViewType` | string |  |
| `productLoadStyle` | string |  |
| `numberOfProductsToLoad` | integer | int32 |
| `showSavingsAmount` | boolean |  |
| `showSavingsPercent` | boolean |  |
| `realTimePricing` | boolean |  |
| `realTimeInventory` | boolean |  |
| `inventoryIncludedWithPricing` | boolean |  |
| `storefrontAccess` | string |  |
| `canShowPriceFilters` | boolean |  |
| `canSeeProducts` | boolean |  |
| `canSeePrices` | boolean |  |
| `canAddToCart` | boolean |  |
| `pricingService` | string |  |
| `displayAttributesInTabs` | boolean |  |
| `attributesTabSortOrder` | string |  |
| `displayDocumentsInTabs` | boolean |  |
| `documentsTabSortOrder` | string |  |
| `displayInventoryPerWarehouse` | boolean |  |
| `displayInventoryPerWarehouseOnlyOnProductDetail` | boolean |  |
| `displayFacetsForStockedItems` | boolean |  |
| `imageProvider` | string |  |
| `catalogUrlPath` | string |  |
| `enableVat` | boolean |  |
| `vatPriceDisplay` | string |  |
| `enableProductRecommendations` | boolean |  |
| `peeriusTrackingUrl` | string |  |
| `peeriusSiteName` | string |  |
| `peeriusApiVersion` | string |  |
| `enablePeeriusRequestsConsoleLogs` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/settings/mobileapp

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `MobileAppSettingsModel` |

##### Response Schema: `MobileAppSettingsModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `startingCategoryForBrowsing` | string | uuid |
| `hasCheckout` | boolean |  |
| `overrideCheckoutNavigation` | boolean |  |
| `checkoutUrl` | string |  |
| `addToCartInProductList` | boolean |  |
| `properties` | object |  |

---


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/settings`

**Child / sub-resources:**

- `/api/v1/settings/account`
- `/api/v1/settings/cart`
- `/api/v1/settings/mobileapp`
- `/api/v1/settings/products`
- `/api/v1/settings/quote`
- `/api/v1/settings/website`
- `/api/v1/settings/wishlist`



---

## Websites

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/websites/current/countries`](#get-api-v1-websites-current-countries)
- [`GET /api/v1/websites/current/countries/{countryId}`](#get-api-v1-websites-current-countries-countryid)
- [`GET /api/v1/websites/current`](#get-api-v1-websites-current)
- [`GET /api/v1/websites/current/sitemessages`](#get-api-v1-websites-current-sitemessages)
- [`GET /api/v1/websites/current/states`](#get-api-v1-websites-current-states)
- [`GET /api/v1/websites/current/states/{stateId}`](#get-api-v1-websites-current-states-stateid)
- [`GET /api/v1/websites/current/languages`](#get-api-v1-websites-current-languages)
- [`GET /api/v1/websites/current/languages/{languageId}`](#get-api-v1-websites-current-languages-languageid)
- [`GET /api/v1/websites/current/addressfields`](#get-api-v1-websites-current-addressfields)
- [`GET /api/v1/websites/current/currencies`](#get-api-v1-websites-current-currencies)
- [`GET /api/v1/websites/current/currencies/{currencyId}`](#get-api-v1-websites-current-currencies-currencyid)
- [`GET /api/v1/websites/current/crosssells`](#get-api-v1-websites-current-crosssells)

---

### `GET` /api/v1/websites/current/countries

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CountryCollectionModel` |

##### Response Schema: `CountryCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `countries` | CountryModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/countries/{countryId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `countryId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CountryModel` |

##### Response Schema: `CountryModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `abbreviation` | string |  |
| `states` | StateModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `WebsiteModel` |

##### Response Schema: `WebsiteModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `countriesUri` | string |  |
| `statesUri` | string |  |
| `languagesUri` | string |  |
| `currenciesUri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `key` | string |  |
| `description` | string |  |
| `isActive` | boolean |  |
| `isRestricted` | boolean |  |
| `websiteFavicon` | string |  |
| `mobilePrimaryColor` | string |  |
| `mobilePrivacyPolicyUrl` | string |  |
| `mobileTermsOfUseUrl` | string |  |
| `companyName` | string |  |
| `companyLogoImagePath` | string |  |
| `companyUrl` | string |  |
| `companyPhone` | string |  |
| `companySocialAccounts` | string |  |
| `address1` | string |  |
| `address2` | string |  |
| `city` | string |  |
| `state` | string |  |
| `postalCode` | string |  |
| `companyCountry` | string |  |
| `countries` | CountryCollectionModel |  |
| `states` | StateCollectionModel |  |
| `languages` | LanguageCollectionModel |  |
| `currencies` | CurrencyCollectionModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/sitemessages

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.name` | string | ❌ |  |
| `parameter.languageCode` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `SiteMessageCollectionModel` |

##### Response Schema: `SiteMessageCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `siteMessages` | SiteMessageModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/states

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `StateCollectionModel` |

##### Response Schema: `StateCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `states` | StateModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/states/{stateId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `stateId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `StateModel` |

##### Response Schema: `StateModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `name` | string |  |
| `abbreviation` | string |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/languages

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `LanguageCollectionModel` |

##### Response Schema: `LanguageCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `languages` | LanguageModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/languages/{languageId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `languageId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `LanguageModel` |

##### Response Schema: `LanguageModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `languageCode` | string |  |
| `cultureCode` | string |  |
| `description` | string |  |
| `imageFilePath` | string |  |
| `currencyPositioning` | string |  |
| `languageTag` | string |  |
| `isDefault` | boolean |  |
| `isLive` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/addressfields

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `AddressFieldCollectionModel` |

##### Response Schema: `AddressFieldCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `billToAddressFields` | AddressFieldDisplayCollectionModel |  |
| `shipToAddressFields` | AddressFieldDisplayCollectionModel |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/currencies

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CurrencyCollectionModel` |

##### Response Schema: `CurrencyCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `currencies` | CurrencyModel[] |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/currencies/{currencyId}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `currencyId` | string | ✅ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `CurrencyModel` |

##### Response Schema: `CurrencyModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `id` | string |  |
| `currencyCode` | string |  |
| `description` | string |  |
| `currencySymbol` | string |  |
| `isDefault` | boolean |  |
| `properties` | object |  |

---

### `GET` /api/v1/websites/current/crosssells

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

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


---

### Relationships

#### Resource Hierarchy

**Parent resources:**

- `/api/v1/websites/current`
- `/api/v1/websites/current/countries`
- `/api/v1/websites/current/currencies`
- `/api/v1/websites/current/languages`
- `/api/v1/websites/current/states`

**Child / sub-resources:**

- `/api/v1/websites/current/addressfields`
- `/api/v1/websites/current/countries`
- `/api/v1/websites/current/crosssells`
- `/api/v1/websites/current/currencies`
- `/api/v1/websites/current/languages`
- `/api/v1/websites/current/sitemessages`
- `/api/v1/websites/current/states`
- `/api/v1/websites/current/countries/{countryId}`
- `/api/v1/websites/current/currencies/{currencyId}`
- `/api/v1/websites/current/languages/{languageId}`
- `/api/v1/websites/current/states/{stateId}`

#### Shared Models

These response/request models are also used by other API sections:

| Model | Also used in |
|-------|--------------|
| `CrossSellCollectionModel` | Products |



---

## Locale

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`POST /api/v1/locale`](#post-api-v1-locale)

---

### `POST` /api/v1/locale

**Auth required:** ❌ No

**Content-Type:** application/json, text/json, application/xml, text/xml, application/x-www-form-urlencoded, text/html  
**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Request Body

**Schema:** `Extensions.Models.UpdateLocaleModel`

| Property | Type | Description |
|----------|------|-------------|
| `countryId` | string | uuid |
| `languageId` | string | uuid |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `object` |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Translationdictionaries

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/translationdictionaries`](#get-api-v1-translationdictionaries)

---

### `GET` /api/v1/translationdictionaries

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parameter.keyWord` | string | ❌ |  |
| `parameter.source` | string | ❌ |  |
| `parameter.languageCode` | string | ❌ |  |
| `parameter.page` | integer (int32) | ❌ |  |
| `parameter.pageSize` | integer (int32) | ❌ |  |
| `parameter.sort` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `TranslationDictionaryCollectionModel` |

##### Response Schema: `TranslationDictionaryCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `translationDictionaries` | TranslationDictionaryModel[] |  |
| `pagination` | PaginationModel |  |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Dashboardpanels

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/dashboardpanels`](#get-api-v1-dashboardpanels)

---

### `GET` /api/v1/dashboardpanels

**Auth required:** ✅ Yes ()

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `DashboardPanelCollectionModel` |

##### Response Schema: `DashboardPanelCollectionModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `dashboardPanels` | DashboardPanelModel[] |  |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

## Mobilecontent

**Base URL:** `https://sonicequipment.commerce.insitesandbox.com`  
**Auth:** API key via query parameter `access_token`

### Endpoints

- [`GET /api/v1/mobilecontent/{PageName}`](#get-api-v1-mobilecontent-pagename)

---

### `GET` /api/v1/mobilecontent/{PageName}

**Auth required:** ❌ No

**Accept:** application/json, text/json, application/xml, text/xml, text/html

#### Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `PageName` | string | ✅ |  |

#### Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `mobileContentParameter.pageName` | string | ❌ |  |

#### Responses

| Status | Description | Schema |
|--------|-------------|--------|
| `200` | OK | `MobileContentModel` |

##### Response Schema: `MobileContentModel`

| Property | Type | Description |
|----------|------|-------------|
| `uri` | string |  |
| `page` | MobilePageDto |  |
| `widgets` | MobileWidgetDto[] |  |
| `properties` | object |  |

---


---

### Relationships

_No cross-endpoint relationships detected for this section._


---

