Public API Reference
====================

> [Home](index.md) ▸ [Public API](index.md#Public_API) ▸ **Reference**

* [addChatId](public-api-reference.md#addChatId) - add a chatid to the Experts List
* [addChannel](public-api-reference.md#addChannel) - add a channel to the Experts List
* [addProduct](public-api-reference.md#addProduct) - add a chatid via product metadata
* [addBrand](public-api-reference.md#addBrand) - add a chatid via brand name
* [addCTA](public-api-reference.md#addCTA) - add a call to action
* [hookEvents](public-api-reference.md#hookEvents) - hook into Chatbar internal events

Adding to the Experts List
--------------------------

#### addChatId

CID.q.push(['**addChatId**', *chatid*]

`chatid` must be a string or an object with a `chatid` field.

#### addChannel

CID.q.push(['**addChannel**', *chatid*]

The same as `addChatId` but it will be displayed with a star symbol at the top of the
Experts List.

#### addProduct

CID.q.push(['**addProduct**', *productData*]

`productData` must be an object with a `brand` field. Chatbar will map this `brand` string
to it's corresponding unique chat handle and add it to the Experts List.

#### addBrand

CID.q.push(['**addBrand**', *brand*]

Chatbar will map `brand` to it's corresponding unique chat handle and add it to the Experts
List.

Configure CTAs
--------------

#### addCTA

CID.q.push(['**addCTA**', *cta*]

`cta` should be an object with `chatid`, `container`, and `settings` fields.

* `chatid` must be the unique brand identifier to which this CTA is tied.
* `container` may be a DOM element or a jQuery selector string.
* `settings` should be an object with a `template` field.
* `template` must be a string of HTML to inject within `container`. It may also be a
JavaScript template for use with [_.template](http://underscorejs.org/#template). It
will be rendered with the following metadata for its context:

```javascript
{
  active: false, // whether the user already has an active conversation with this `chatid`
  available: true, // whether any agents are available
  label: 'Acer', // presentable display name for this `chatid`
  channel: false // boolean to specify if this chatid is owned by the hosting channel
}
```

In the following example we append a CTA to some element with an ID of `product-details`,
using dynamic text within the button:

```javascript
var container = document.createElement('div');
document.getElementById('product-details').appendChild(container);
CID.q.push(['addCTA', {
  chatid: 'acer',
  container: container,
  settings: {
    template: "<button class='chatid-cta'>Chat with <%= this.label %></button>"
  }
}])
```

[View demo](https://s3.amazonaws.com/chatid-mojo/g/context/docs-cta/index.html)
