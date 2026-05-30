# Shopify Geo Personalizer

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Shopify](https://img.shields.io/badge/Shopify-Liquid-green.svg)
![Status](https://img.shields.io/badge/status-production--ready-brightgreen.svg)
![Zero Apps](https://img.shields.io/badge/apps-zero%20dependencies-brightgreen.svg)

A dynamic geo-based personalization engine for Shopify storefronts. Serves location-specific content, currency, and offers natively without third party apps or redirect bloat.

---

## The Problem This Solves

Most Shopify stores show the same content to every visitor regardless of where they are. A customer in Lagos sees the same homepage as a customer in London. No localized offers, no currency switching, no region-specific messaging. Generic geo apps fix this by adding redirect layers that slow your store and break mobile funnels. This engine does it natively inside your Liquid theme.

---

## Architecture

```mermaid
graph TD
    A[Visitor Lands on Store] --> B[Detect IP Location]
    B --> C{Route by Region}
    C -->|Nigeria / Africa| D[Show NGN Pricing & Local Offer]
    C -->|UK / Europe| E[Show GBP Pricing & EU Offer]
    C -->|US / Canada| F[Show USD Pricing & NA Offer]
    C -->|Asia Pacific| G[Show Regional Currency & Offer]
    D & E & F & G --> H[Render Localized Content]
    H --> I[Zero Redirect Overhead]
```

---

## Features

| Feature | Description |
|---|---|
| IP based detection | Detects visitor country on server side |
| Currency routing | Displays correct currency per region |
| Localized offers | Shows region specific banners and messaging |
| Hreflang support | Correct SEO signals per region |
| Zero redirects | No app layer, no redirect chains |
| Mobile optimized | No layout shift on geo content swap |

---

## Sample Liquid Implementation

**Region based content rendering:**
```liquid
{% assign country = localization.country.iso_code %}

{% case country %}
  {% when 'NG', 'GH', 'KE', 'ZA' %}
    <div class="geo-banner africa">
      <p>🌍 Free shipping across Africa on orders over ₦50,000</p>
    </div>
    {% assign local_currency = 'NGN' %}

  {% when 'GB', 'DE', 'FR', 'NL' %}
    <div class="geo-banner europe">
      <p>🇪 Free EU shipping on orders over £75</p>
    </div>
    {% assign local_currency = 'GBP' %}

  {% when 'US', 'CA' %}
    <div class="geo-banner north-america">
      <p>🇺🇸 Free US shipping on orders over $100</p>
    </div>
    {% assign local_currency = 'USD' %}

  {% else %}
    <div class="geo-banner global">
      <p>🌐 Worldwide shipping available at checkout</p>
    </div>
{% endcase %}
```

---

## Quick Start

```bash
git clone https://github.com/Waynelynx12/shopify-geo-personalizer.git
```

Copy snippets into your Shopify theme under **Online Store > Themes > Edit Code > Snippets** and render using:

```liquid
{% render 'geo-banner' %}
{% render 'geo-currency-router' %}
```

---

## Environment Setup

Enable Shopify Markets in your store under **Settings > Markets** before implementing geo routing. This unlocks the localization object used throughout this library.

---

## Built By

Sheriff Wayne, Growth Engineer and Shopify Technical Specialist. I build native geo personalization systems for international ecommerce stores that need localized experiences without app dependency or redirect overhead.
