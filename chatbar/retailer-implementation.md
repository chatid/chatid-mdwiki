Retailer Implementation Guide
=============================

> [Home](index.md) ▸ [Implementation Guides](index.md#Implementation Guides) ▸ **For Retailers**

Before following this guide, be sure to review [Getting Started](getting-started.md) and
[Public API Basics](public-api-overview.md#Basics).

This guide will cover a few use-cases for Chatbar on a retail website:

* [Product Detail Pages](retailer-implementation.md#Product_Detail_Pages) - add a CTA to your product detail pages
* [Confirmation Page Logging](retailer-implementation.md#Confirmation_Page) - log conversions from your confirmation page

#### Product Detail Pages (PDPs)

A common use-case for Chatbar on retail websites is a brand-specific call-to-action (CTA)
on product detail pages.

First, add a CTA container element (the `id` can be anything you'd like):

```
<div id='chatid-cta-pdp'></div>
```

Next, call [mapProduct](public-api-reference.md#mapProduct) with product metadata and a
callback function that calls [addCTA](public-api-reference.md#addCTA). For example:

```javascript
CID.q.push(['mapProduct', {
  brand: 'Ergotron',
  merchant_sku: 'N82E16824994063',
  model: '45-241-026',
  name: 'LX Desk Mount LCD Arm',
  price: '109.99',
  currency: 'USD',
  tags: ['PCs & Laptops', 'Desktop PCs', 'Monitors', 'Monitor Accessories', 'Ergotron']
}, function(chatid) {
  CID.q.push(['addCTA', {
    chatid: chatid,
    container: '#chatid-cta-pdp',
    settings: {
      template: "<button data-ref='button'>Chat with Ergotron</button>"
    }
  }]);
}]);
```

*Reference*: [mapProduct](public-api-reference.md#mapProduct),
[addCTA](public-api-reference.md#addCTA)

**NOTE:** Product mapping will only work *after* ChatID has configured your embed code
and only for mapping ChatID-enabled brands.

**NOTE:** This snippet should be placed across all PDPs. For pages that feature vendors
that are not yet ChatID-enabled, CTAs will simply not display.

#### Confirmation Page

On your confirmation page, use the [log](public-api-reference.md#log) API call with
the `'conversion'` event. Use additional arguments to pass in all products purchased by
the user:

```javascript
CID.q.push(['log', 'conversion', {
    brand: 'Acer',
    merchant_sku: '123456',
    model: 'ABCDEF',
    name: 'Aspire A7',
    quantity: 1,
    total_price: '349.99',
    currency: 'USD',
    tags: ['PCs & Laptops', 'Laptops']
  }, {
    brand: 'Seagate',
    merchant_sku: '654321',
    model: 'ABCDEF',
    name: '500GB External HDD',
    quantity: 1,
    total_price: '43.99',
    currency: 'USD',
    tags: ['Computer Hardware', 'Hard Drives', 'Internal Hard Drives']
  }
  // ... use additional arguments for each product purchased
]);
```

*Reference*: [log](public-api-reference.md#log)

#### Next

* Browse [Examples](demos.md)
* Read the [API Overview](public-api-overview.md)
* Explore the [API Reference](public-api-reference.md)
