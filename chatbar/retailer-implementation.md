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
CID('ctas.insert', {
  chatid: 'ergotron',
  container: '#chatid-cta-pdp',
  settings: {
    template: "<button data-ref='button'>Chat with Ergotron</button>"
  }
});
```

*Reference*: [ctas.insert](public-api-reference.md#ctas.insert)

**(2) I do not have the `chatid`, and need to obtain it by mapping the brand name**

As part of your Chatbar implementation, ChatID can help map your brand ids to the vendor's
`chatid`. Simply call [chatids.lookup.byBrand](public-api-reference.md#chatids.lookup.byBrand) with the name of the
brand and provide a callback function for obtaining the `chatid`, which you can then pass
to [ctas.insert](public-api-reference.md#ctas.insert). For example:

```javascript
CID('chatids.lookup.byBrand', 'Ergotron', function(chatid) {
  CID('ctas.insert', {
    chatid: chatid,
    container: '#chatid-cta-pdp',
    settings: {
      template: "<button data-ref='button'>Chat with Ergotron</button>"
    }
  });
});
```

*Reference*: [chatids.lookup.byBrand](public-api-reference.md#chatids.lookup.byBrand),
[ctas.insert](public-api-reference.md#ctas.insert)

**NOTE:** Brand mapping will only work *after* ChatID has configured your embed code
and only for mapping ChatID-enabled brands.

#### Product Detail Page Logging

On product detail pages, use the [events.log](public-api-reference.md#events.log) API call with
the `'product'` event:

```javascript
CID('events.log', 'product', {
  brand: 'Ergotron',
  merchant_sku: 'N82E16824994063',
  model: '45241026',
  name: 'LX Desk Mount LCD Arm',
  sale_price: '109.99',
  unit_price: '109.99',
  currency: 'USD',
  tags: ['PCs & Laptops', 'Desktop PCs', 'Monitors', 'Monitor Accessories', 'Ergotron']
});
```

*Reference*: [events.log - product](public-api-reference.md#events.log_-_product)

#### Confirmation Page Logging

On your confirmation page, use the [events.log](public-api-reference.md#events.log) API call with
the `'conversion'` event. Use additional arguments to pass in all products purchased by
the user:

```javascript
CID('events.log', 'conversion', {
    brand: 'Acer',
    merchant_sku: '123456',
    model: 'ABCDEF',
    name: 'Aspire A7',
    quantity: 1,
    sale_price: '349.99',
    unit_price: '349.99',
    currency: 'USD',
    tags: ['PCs & Laptops', 'Laptops']
  }, {
    brand: 'Seagate',
    merchant_sku: '654321',
    model: 'ABCDEF',
    name: '500GB External HDD',
    quantity: 1,
    sale_price: '38.99',
    unit_price: '43.99',
    currency: 'USD',
    tags: ['Computer Hardware', 'Hard Drives', 'Internal Hard Drives']
  }
  // ... use additional arguments for each product purchased
);
```

*Reference*: [events.log - conversion](public-api-reference.md#events.log_-_conversion)

#### Next

* Browse [Examples](demos.md)
* Read the [API Overview](public-api-overview.md)
* Explore the [API Reference](public-api-reference.md)
