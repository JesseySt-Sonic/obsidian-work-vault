---
tags:
  - control-panel-api
---
# Cache Invalidation Service

`Sonic.ControlPanel.Api` — exposes endpoints to flush and selectively invalidate server-side caches for pages, navigation, content, and configuration.

---

**Auth:** API key via `X-Api-Key` header

| Environment | Base URL |
|-------------|----------|
| Production | `https://control-panel-api-prod.redbay-f1bdfa92.westeurope.azurecontainerapps.io` |

---

## Contents

- [[#Nuke]]
- [[#PDP]]
- [[#PLP]]
- [[#Categories]]
- [[#Country Languages]]
- [[#Announcements]]
- [[#Translations]]
- [[#Navigation]]

---

## Nuke

Flush entire caches in one call.

### `DELETE` /cache

Clears the full cache.

**Auth required:** ✅ Yes

#### Responses

| Status | Description |
|--------|-------------|
| `200` | OK |

---

### `DELETE` /cachenavigation

Clears the navigation cache.

**Auth required:** ✅ Yes

#### Responses

| Status | Description |
|--------|-------------|
| `200` | OK |

---

## PDP

### `POST` /invalidatePDP

Invalidates PDP (Product Detail Page) cache for specific products.

**Auth required:** ✅ Yes

#### Request Body

`string[]` — array of product numbers

```json
["236", "47335", "47363-2"]
```

#### Responses

| Status | Description |
|--------|-------------|
| `200` | OK |

---

## PLP

### `POST` /invalidatePLP

Invalidates PLP (Product Listing Page) cache for specific categories.

**Auth required:** ✅ Yes

#### Request Body

`string[]` — array of category B2B names

```json
["109094", "109294"]
```

#### Responses

| Status | Description |
|--------|-------------|
| `200` | OK |

---

## Categories

### `POST` /InvalidateCategories

Invalidates the categories cache.

**Auth required:** ✅ Yes

#### Responses

| Status | Description |
|--------|-------------|
| `200` | OK |

---

## Country Languages

### `POST` /InvalidateCountryLanguages

Invalidates the country languages cache.

**Auth required:** ✅ Yes

#### Responses

| Status | Description |
|--------|-------------|
| `200` | OK |

---

## Announcements

### `POST` /InvalidateAnnouncements

Invalidates the announcements cache.

**Auth required:** ✅ Yes

#### Responses

| Status | Description |
|--------|-------------|
| `200` | OK |

---

## Translations

### `POST` /InvalidateTranslations

Invalidates the translations cache.

**Auth required:** ✅ Yes

#### Responses

| Status | Description |
|--------|-------------|
| `200` | OK |

---

## Navigation

### `POST` /InvalidateNavigation

Invalidates the navigation cache.

**Auth required:** ✅ Yes

#### Responses

| Status | Description |
|--------|-------------|
| `200` | OK |

---

> **Note:** The spec summary for `/InvalidateTranslations` reads "Invalidate Navigation cache" — likely a copy-paste error. Treated here as translations.
