Retailer Implementation Guide
=============================

> [Home](index.md) ▸ [Implementation Guides](index.md#Implementation Guides) ▸ **For Retailers**

Before following this guide, be sure to review [Getting Started](getting-started.md) and
[Public API Basics](public-api-overview.md#Basics).

This guide will cover a few use-cases for Chatbar on a retail website:

* [Product Detail Page CTA](retailer-implementation.md#Product_Detail_Page_CTA) - add a CTA to your product detail pages
* [Product Detail Page Logging](retailer-implementation.md#Product_Detail_Page_Logging) - log product metadata from your PDPs
* [Confirmation Page Logging](retailer-implementation.md#Confirmation_Page_Logging) - log conversions from your confirmation page

#### Product Detail Page (PDP) CTA

A common use-case for Chatbar on retail websites is a brand-specific call-to-action (CTA)
on product detail pages.

First, add a CTA container element (the `id` can be anything you'd like):

```
<div id='chatid-cta-pdp'></div>
```

Next, you must choose the appropriate strategy for rendering this CTA: **(1)** or **(2)**.

**(1) I know the `chatid` for this brand**

If you have access to the ChatID-specific identifier for this brand (an all lowercase
string), you may add their CTA straight away:

```javascript
CID('addCTA', {
  chatid: 'ergotron',
  container: '#chatid-cta-pdp'
});
```

*Reference*: [addCTA](public-api-reference.md#addCTA)

**(2) I do not have the `chatid`, and need to obtain it by mapping the brand name**

As part of your Chatbar implementation, ChatID can help map your brand ids to the vendor's
`chatid`. Simply call [mapBrand](public-api-reference.md#mapBrand) with the name of the
brand and provide a callback function for obtaining the `chatid`, which you can then pass
to [addCTA](public-api-reference.md#addCTA). For example:

```javascript
CID('mapBrand', 'Ergotron', function(chatid) {
  CID('addCTA', {
    chatid: chatid,
    container: '#chatid-cta-pdp'
  });
});
```

*Reference*: [mapBrand](public-api-reference.md#mapBrand),
[addCTA](public-api-reference.md#addCTA)

**NOTE:** Brand mapping will only work *after* ChatID has configured your embed code
and only for mapping ChatID-enabled brands.

#### Product Detail Page Logging

On product detail pages, use the [log](public-api-reference.md#log) API call with
the `'product'` event:

```javascript
CID('log', 'product', {
  brand: 'Ergotron',
  merchant_sku: 'N82E16824994063',
  model: '45241026',
  name: 'LX Desk Mount LCD Arm',
  price: '109.99',
  currency: 'USD',
  tags: ['PCs & Laptops', 'Desktop PCs', 'Monitors', 'Monitor Accessories', 'Ergotron']
});
```

*Reference*: [log - product](public-api-reference.md#log_-_product)

#### Confirmation Page Logging

On your confirmation page, use the [log](public-api-reference.md#log) API call with
the `'conversion'` event. Use additional arguments to pass in all products purchased by
the user:

```javascript
CID('log', 'conversion', {
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
);
```

*Reference*: [log - conversion](public-api-reference.md#log_-_conversion)

#### Next

* Browse [Examples](demos.md)
* Read the [API Overview](public-api-overview.md)
* Explore the [API Reference](public-api-reference.md)
