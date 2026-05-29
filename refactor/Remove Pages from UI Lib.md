# Remove Pages from UI Lib

> **Status:** Planned — next major version bump. See also [[UI lib data fetching separation]].

The library currently exports ~99 symbols from `src/pages/` — full page assemblies (`OrderHistoryPage`, `CartPage`, etc.) and connected sub-components that inline API calls. Goal is to thin it to pure UI components + API services so the consuming Next.js app can own data fetching via server actions.

**API hooks in `src/shared/api/` stay in the library** — useful for client-side scenarios.

---

## Approach

One breaking major-version bump. Three categories across all `src/pages/` exports:

| Tag | Meaning |
|-----|---------|
| **RELOCATE** | Pure UI, no API calls — move to a new home in `src/` |
| **SPLIT** | Inlines API hooks but the UI is reusable — create pure version (props instead of hooks), then delete connected |
| **DELETE** | Full page assembly or connected component whose pure sibling already exists |

---

## RELOCATE — pure components moving out of `src/pages/`

**→ `src/layout/`**
- `pages/components/page`, `page-container`, `page-meta-data`
- `pages/account/layouts/sign-in-page-layout/*`
- `pages/checkout/layouts/checkout-page-layout/*`
- `pages/my-sonic/layouts/my-sonic-layout/*`
- `pages/product/layouts/product-details-page-layout/*`

**→ `src/forms/`**
- `pages/account/components/sign-in-form`
- `pages/account/components/create-account-form`
- `pages/account/components/change-password-form`
- `pages/my-sonic/actions/upload-order/upload-order-form`

**→ new `src/checkout/`**
- `pages/checkout/shipping-page/shipping-page-content`
- `pages/checkout/order-confirmation-page/order-confirmation-page-content`
- `pages/checkout/payment-page/payment-page-content`
- `pages/checkout/shipping-page/components/readonly-address`, `sonic-address`, `ship-to-mode-selector`, `currency-change-dialog`

**→ new `src/my-sonic/`**
- `pages/my-sonic/navigation/my-sonic-desktop-navigation`, `mobile-navigation`, `navigation-items`
- `pages/my-sonic/actions/change-password/change-password-dialog`
- `pages/my-sonic/actions/change-customer/change-customer-dialog`
- `pages/my-sonic/actions/edit-user-info/edit-user-info`, `edit-user-info-dialog`
- `pages/my-sonic/actions/upload-order/upload-order-instructions`
- `pages/my-sonic/widgets/components/address-data-card`

**→ new `src/product/`**
- `pages/product/components/product-overview`
- `pages/product/product-listing-page/product-listing`
- `pages/product/product-listing-page/no-results/no-results`
- `pages/product/product-listing-page/product-listing-page-data-types`
- `pages/product/product-listing-page/product-listing-page-provider/*`
- `pages/product/product-listing-page/product-listing-product-overview`
- `pages/product/search-result-page/search-result-product-overview`
- `pages/product/search-result-page/search-results-page-category-carousel`

**→ `src/shared/hooks/` and `src/shared/utils/`**
- `pages/checkout/payment-page/hooks/use-get-adyen-redirect-result`, `use-has-returned-from-adyen`
- `pages/checkout/shipping-page/hooks/use-patch-shipping-details`
- `pages/checkout/payment-page/utils/parse-amount`

---

## SPLIT — create pure version, then delete connected

Each pure version replaces every internal hook call with a prop.

| Connected component | What to extract |
|---|---|
| `pages/checkout/shipping-page/components/address-book-selector` | Remove `useFetchPagedShipToAddresses` — accept `addresses` + `pagination` as props |
| `pages/checkout/shipping-page/components/edit-checkout-bill-to-address-form` | Remove `useFetchCurrentCart` — accept `cart` as prop |
| `pages/checkout/payment-page/components/adyen-payment` | Extract UI shell; remove session/config hooks |
| `pages/checkout/payment-page/components/payment` | Extract UI shell; remove `usePatchCart`, `usePlaceOrder` |
| `pages/my-sonic/widgets/connected-address-book-widget` | Pure `AddressBookWidget` — accept `addresses`, `pagination`, callbacks as props |
| `pages/my-sonic/widgets/connected-bill-to-address-widget` | Pure `BillToAddressWidget` |
| `pages/my-sonic/widgets/connected-customer-information-widget` | Pure `CustomerInformationWidget` |
| `pages/my-sonic/widgets/connected-ship-to-address-widget` | Pure `ShipToAddressWidget` |
| `pages/my-sonic/widgets/connected-user-account-widget` | Pure `UserAccountWidget` |
| `pages/my-sonic/actions/create-ship-to-address/connected-create-ship-to-address-form` | Pure `CreateShipToAddressForm` |
| `pages/my-sonic/actions/edit-bill-to-address/connected-edit-bill-to-address-form` | Pure `EditBillToAddressForm` |
| `pages/my-sonic/actions/edit-ship-to-address/connected-edit-ship-to-address-form` | Pure `EditShipToAddressForm` |
| `pages/my-sonic/navigation/connected-my-sonic-navigation` | Pure nav already exists — just delete connected |

---

## DELETE — page assemblies (no pure version needed)

All top-level `*Page` components go away. The Next.js app replaces these with server components:

`SignInPage`, `ChangePasswordPage`, `CreateAccountPage`, `CartPage`, `ShippingPage`, `PaymentPage`, `OrderConfirmationPage`, `CountriesPage`, `ErrorPage`, `LoadingPage`, `FavoritesPage`, `MyAccountPage`, `OrderDetailsPage`, `OrderHistoryPage`, `UploadOrderPage`, `CreateShipToAddressDetailsPage`, `EditBillToAddressDetailsPage`, `EditShipToAddressDetailsPage`, `ProductDetailsPage`, `ProductListingPage`, `SearchResultsPage`

Also delete: `pages/my-sonic/actions/change-password/change-password` and `change-customer/change-customer` orchestrators.

---

## Execution steps

1. Audit every line in `src/exports.ts` (lines 290–388) — assign RELOCATE / SPLIT / DELETE
2. Create new target dirs: `src/checkout/`, `src/my-sonic/`, `src/product/`
3. Relocate all RELOCATE files (move file + css module + stories, fix imports, update exports.ts)
4. For each SPLIT: create pure component alongside connected file → delete connected → update exports.ts
5. Delete all page assemblies → remove `src/pages/`
6. Bump `package.json` to next major version
7. `pnpm test:types && pnpm test:unit && pnpm build` — must all pass

---

## Key files

- `src/exports.ts` lines 290–388 — primary file to update
- `src/shared/api/` — untouched; stays in library
- `package.json` — major version bump
