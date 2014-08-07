Public API Reference
====================

> [Chatbar](index.md) ▸ [Public API](index.md#Public_API) ▸ **Reference**

* [chatids.add](public-api-reference.md#chatids.add) - add a chatid to the Experts List
* [chatids.addChannel](public-api-reference.md#chatids.addChannel) - add a channel to the Experts List
* [chatids.lookup.byBrand](public-api-reference.md#chatids.lookup.byBrand) - add a chatid via brand name
* [ctas.insert](public-api-reference.md#ctas.insert) - add a call to action
* [events.log](public-api-reference.md#events.log) - log events for ChatID analysis

Adding to the Experts List
--------------------------

#### chatids.add

CID('**chatids.add**', *chatid*)

Add a chatid to the Experts List. `chatid` must be a string or an object with a `chatid`
field.

#### chatids.addChannel

CID('**chatids.addChannel**', *chatid*)

The same as `chatids.add` but will be displayed with a star symbol at the top of the
Experts List to indicate an expert from the host website.

#### chatids.lookup.byBrand

CID('**chatids.lookup.byBrand**', *brandName*, *callback*)

Add a chatid to the Experts List using the brand name. Chatbar will use this metadata to
determine the brand's unique chat handle (if it's ChatID-enabled) and add it to the
Experts List.

`callback` is an optional function to be called if the brand is ChatID-enabled. The first
argument will be the unique `chatid` handle for the given brand:

```javascript
CID('chatids.lookup.byBrand', /* brandName */, function(chatid) { // callback will fire if this brand is ChatID-enabled, with the `chatid` handle for the first argument
  // perform additional actions with this identifier, such as adding a CTA
});
```

[View demo](http://demo.chatid.com/chatbar/docs-map-brand/index.html)

Configure CTAs
--------------

#### ctas.insert

CID('**ctas.insert**', *cta*)

Add a call to action to the page. `cta` should be an object with the following structure:

```javascript
{
  chatid: 'acer', // the unique brand identifier to which this CTA is tied
  container: '#chatid-cta', // a DOM element or a jQuery selector string
  settings: { // an object with a `template` field
    // HTML to inject within `container`, the clickable element must specify data-ref='button'
    template: "<button data-ref='button'>Chat now</button>"
  }
}
```

`template` may also be a JavaScript template for use with
[_.template](http://underscorejs.org/#template). It will be rendered with the following
metadata for its context:

```javascript
{
  active: false, // whether the user already has an active conversation with this `chatid`
  available: true, // whether any agents are available
  label: 'Acer', // presentable display name for this `chatid`
  channel: false // boolean to specify if this chatid is owned by the hosting channel
}
```

`ctas.insert` will call `chatids.add` internally if you haven't done so already.

In the following example we append a CTA to some element with an ID of `chatid-cta`,
using dynamic text within the button:

```javascript
CID('ctas.insert', {
  chatid: 'chatid.echo',
  container: 'chatid-cta',
  settings: {
    template: "<button data-ref='button'>Chat with <%= this.label %></button>"
  }
});
```

[View demo](http://demo.chatid.com/chatbar/docs-cta/index.html)

Logging Events
--------------

#### events.log

CID('**events.log**', *eventName*, *args...*)

Log events for collecting metrics and analytics. `eventName` will be the key for which
this unique behavior will be indexed. `args` may be any number of additional arguments
relevant to the event.

#### events.log - product

CID('**events.log**', '**product**', *productData*)

Here is an example using the `events.log` method to send Chatbar metadata on a PDP:

```javascript
CID('events.log', 'product', {
  brand: 'Seagate', // brand name
  merchant_sku: '654321', // retailer-specific SKU
  model: 'ABCDEF', // vendor-provided model number/identifier
  name: '500GB External HDD', // product name
  sale_price: '38.99', // current product price (sale price if it's on sale)
  unit_price: '43.99', // base product price (opposed to sale price)
  currency: 'USD', // currency for price
  tags: ['Computer Hardware', 'Hard Drives', 'Internal Hard Drives'] // an array of tags that describe the product
});
```

#### events.log - conversion

CID('**events.log**', '**conversion**', *productData1*, *productData2*, ...)

Here is an example using the `events.log` method to send Chatbar a conversion event:

```javascript
CID(
  'events.log', // 1st param is the API method, in this case it's 'events.log'
  'conversion', // 2nd param is first argument to the 'events.log' method, in this case it's 'conversion'
  { // 3rd param is the 2nd argument to the 'events.log' method, in this case, the 1st of 2 products purchased
    brand: 'Acer',
    merchant_sku: '123456',
    model: 'ABCDEF',
    name: 'Aspire A7',
    quantity: 1,
    sale_price: '349.99',
    unit_price: '349.99',
    currency: 'USD',
    tags: ['PCs & Laptops', 'Laptops']
  }, { // etc
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
);
```

**HINT:** for the `'conversion'` event, product objects should follow the same structure
as used with the 'product' event, with the addition of the `quantity` field.

If this snippet were to be placed on your site's confirmation page, ChatID would be able
to associate the purchase with any chats this user may have participated in during his or
her shopping experience.
