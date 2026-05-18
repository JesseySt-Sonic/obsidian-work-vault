
> **For:** Customer Support reps handling tickets where a customer says the Sonic Equipment website is broken on their phone or computer.
>
> **What this is:** A short cheat sheet for the most common cases where the problem is **not** a bug we can fix — it's the customer's browser, app, or an extension. Each case has a ready-to-send reply.
>
> **Last updated:** 2026-05-13.
>
> **Tech reference for engineers:** see [SD-623](https://sonic-equipment.atlassian.net/browse/SD-623) for the technical detail behind each case.

## How to use this page

When a customer reports a problem, find the row in the table below that best matches what they describe, then follow the link to the matching section for the full reply.

| What the customer says                                              | Most likely cause                              | Go to                                                    |
| ------------------------------------------------------------------- | ---------------------------------------------- | -------------------------------------------------------- |
| "I tapped a link from Facebook and the page is blank or won't load" | They are stuck in Facebook's in-app browser    | [Case 1](#case-1--customer-came-from-a-facebook-ad)      |
| "After I clicked the cookie banner, the page froze / went blank"    | The cookie banner is conflicting with the site | [Case 2](#case-2--page-broke-after-the-cookie-banner)    |
| "The site crashed when I tapped a product / category" on phone      | A browser extension is interfering             | [Case 3](#case-3--page-crashed-mid-navigation-on-mobile) |
If none of these match, treat it as a real bug and escalate to engineering.

---

## Case 1 — Customer came from a Facebook ad

**What's happening:** Some customers tap a Facebook ad on their phone and end up viewing our site inside Facebook's own little browser (the one that lives inside the Facebook app). That browser injects its own tracking code, which doesn't always work on outside sites and can cause the page to look broken.

**How to spot it in the ticket:**

- They mention they came from Facebook or Instagram.
- They're on an iPhone or iPad.
- The link they clicked has `utm_source=Meta` or `fbclid=` in it.

**What to reply:**

> Thanks for letting us know! It looks like you opened the link from inside the Facebook app. That app has its own built-in browser that doesn't always play nicely with outside websites.
>
> Could you try this:
>
> 1. Go back to the page on Facebook
> 2. Tap the three-dot menu (⋯) in the top-right corner
> 3. Choose **"Open in Safari"** (or **"Open in Chrome"**)
>
> The page should work normally from there. Let us know if it still doesn't!

---

## Case 2 — Page broke after the cookie banner

**What's happening:** Our cookie consent banner (the one that pops up the first time you visit) can occasionally clash with the rest of the site and cause it to freeze or go blank. We know about this and engineering is working on a fix.

**How to spot it in the ticket:**

- The customer specifically mentions the cookie pop-up or accepting/declining cookies.
- They say the page went blank, froze, or stopped responding right after.
- More common on Android (Samsung Internet, Chrome on Android) but can happen anywhere.

**What to reply:**

> Sorry about that! We're aware of an issue where our cookie banner can occasionally cause the page to freeze, and our team is actively working on a fix.
>
> In the meantime, this usually clears it up:
>
> 1. Clear the cookies for `sonic-equipment.com` in your browser settings
> 2. Reload the page
>
> If that still doesn't work, please try a different browser (e.g. Chrome if you were on Samsung Internet, or vice versa). Let us know which device and browser you're using so we can pass it on to the team.

---

## Case 3 — Page crashed mid-navigation on mobile

**What's happening:** Some browser add-ons (translation tools, ad blockers, password managers, accessibility helpers) modify pages as they load. On our site, this can cause the page to crash when the customer taps a link to go from one page to another.

**How to spot it in the ticket:**

- The customer is on mobile (usually Android Chrome).
- They say the site crashed *while* they were navigating, not on the first load.
- It often happens after they tap an old bookmark or an old search result (URLs containing `/Catalog/`).

**What to reply:**

> Sorry you ran into this! This kind of crash is usually caused by a browser add-on (such as a translation tool, ad blocker, password manager, or accessibility extension) interfering with the page.
>
> Could you try:
>
> 1. Disable any add-ons or extensions you have installed in your browser
> 2. Or open the site in a private/incognito window (which usually disables extensions)
> 3. Reload and try again
>
> If the problem only happens with extensions on, that confirms it. If it still happens with everything disabled, please reply with which device and browser you're using and we'll investigate further.

---

## When to escalate to engineering

If a customer ticket doesn't fit any of the four cases above, treat it as a real bug:

- Get the device + browser (e.g. "iPhone 14, Safari").
- Get the exact URL they were on (or a screenshot of the address bar).
- Get a description of the steps they took.
- Forward to Theo for triage.

## Updates to this page

This page is maintained by engineering and will get new cases added as we identify new patterns. If you notice a recurring symptom that isn't on this page, please flag it.

---

### For engineers

The Sentry signatures, stack traces, browser version tags, and proposed inbound filters that map to these four cases live in [SD-623](https://sonic-equipment.atlassian.net/browse/SD-623). Real (non-third-party) bugs from the same incident are in [SD-620](https://sonic-equipment.atlassian.net/browse/SD-620), [SD-621](https://sonic-equipment.atlassian.net/browse/SD-621), [SD-622](https://sonic-equipment.atlassian.net/browse/SD-622). Umbrella: [SD-594](https://sonic-equipment.atlassian.net/browse/SD-594).
