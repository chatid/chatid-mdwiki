Public API Reference
====================

> [Home](index.md) ▸ [Public API](index.md#Public_API) ▸ **Reference**

* [addChatId](public-api-reference.md#addChatId) - add a chatid to the Experts List
* [addChannel](public-api-reference.md#addChannel) - add a channel to the Experts List
* [mapProduct](public-api-reference.md#mapProduct) - add a chatid via product metadata
* [addCTA](public-api-reference.md#addCTA) - add a call to action
* [log](public-api-reference.md#log) - log events for ChatID analysis

Adding to the Experts List
--------------------------

#### addChatId

CID.q.push(['**addChatId**', *chatid*])

Add a chatid to the Experts List. `chatid` must be a string or an object with a `chatid`
field.

#### addChannel

CID.q.push(['**addChannel**', *chatid*])

The same as `addChatId` but will be displayed with a star symbol at the top of the
Experts List to indicate an expert from the host website.

#### mapProduct

CID.q.push(['**mapProduct**', *productData*, *callback*])

Add a chatid to the Experts List using product metadata. `productData` must be an object
with the following structure:

```javascript
{
  brand: 'Seagate', // brand name
  merchant_sku: '654321', // retailer-specific SKU
  model: 'ABCDEF', // vendor-provided model number/identifier
  name: '500GB External HDD', // product name
  price: '43.99', // current product price (sale price if it's on sale)
  currency: 'USD', // currency for price
  tags: ['Computer Hardware', 'Hard Drives', 'Internal Hard Drives'] // an array of tags that describe the product
}
```

Chatbar will use this metadata to determine the brand's unique chat handle (if it's
ChatID-enabled) and add it to the Experts List.

`callback` is an optional function to be called if the brand is ChatID-enabled. The first
argument will be the unique `chatid` handle for the given brand:

```javascript
var CID = (CID && CID.q) ? CID : { q: [] };
CID.q.push(['mapProduct', {
  // productData ...
}, function(chatid) { // callback will fire if this brand is ChatID-enabled, passing the `chatid` handle
  // perform additional actions with this identifier, such as adding a CTA
}]);
```

[View demo](https://s3.amazonaws.com/chatid-mojo/g/context/docs-map-product/index.html)

Configure CTAs
--------------

#### addCTA

CID.q.push(['**addCTA**', *cta*])

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

`addCTA` will call `addChatId` internally if you haven't done so already.

In the following example we append a CTA to some element with an ID of `chatid-cta`,
using dynamic text within the button:

```javascript
CID.q.push(['addCTA', {
  chatid: 'chatid.echo',
  container: 'chatid-cta',
  settings: {
    template: "<button data-ref='button'>Chat with <%= this.label %></button>"
  }
}]);
```

[View demo](https://s3.amazonaws.com/chatid-mojo/g/context/docs-cta/index.html)

Logging Events
--------------

#### log

CID.q.push(['**log**', *eventName*, *args...*])

Log events for collecting metrics and analytics. `eventName` will be the key for which
this unique behavior will be indexed. `args` may be any number of additional arguments
relevant to the event.

Here is an example using the `log` method to send Chatbar a conversion event:

```javascript
CID.q.push([
  'log', // 1st param is the API method, in this case it's 'log'
  'conversion', // 2nd param is first argument to the 'log' method, in this case it's 'conversion'
  { // 3rd param is the 2nd argument to the 'log' method, in this case, the 1st of 2 products purchased
    brand: 'Acer',
    merchant_sku: '123456',
    model: 'ABCDEF',
    name: 'Aspire A7',
    price: '349.99',
    currency: 'USD',
    tags: ['PCs & Laptops', 'Laptops']
  }, { // etc
    brand: 'Seagate',
    merchant_sku: '654321',
    model: 'ABCDEF',
    name: '500GB External HDD',
    price: '43.99',
    currency: 'USD',
    tags: ['Computer Hardware', 'Hard Drives', 'Internal Hard Drives']
  }
]);
```

If this snippet were to be placed on your site's confirmation page, ChatID would be able
to associate the purchase with any chats this user may have participated in during his or
her shopping experience.
