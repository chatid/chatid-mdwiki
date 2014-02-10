Public API Reference
====================

> [Home](index.md) ▸ [Public API](index.md#Public_API) ▸ **Reference**

* [addChatId](public-api-reference.md#addChatId) - add a chatid to the Experts List
* [addChannel](public-api-reference.md#addChannel) - add a channel to the Experts List
* [addProduct](public-api-reference.md#addProduct) - add a chatid via product metadata
* [addBrand](public-api-reference.md#addBrand) - add a chatid via brand name
* [addCTA](public-api-reference.md#addCTA) - add a call to action
* [log](public-api-reference.md#log) - send events to Chatbar

Adding to the Experts List
--------------------------

#### addChatId

CID.q.push(['**addChatId**', *chatid*])

`chatid` must be a string or an object with a `chatid` field.

#### addChannel

CID.q.push(['**addChannel**', *chatid*])

The same as `addChatId` but it will be displayed with a star symbol at the top of the
Experts List.

#### addProduct

CID.q.push(['**addProduct**', *productData*])

`productData` must be an object with a `brand` field. Chatbar will map this `brand` string
to it's corresponding unique chat handle and add it to the Experts List.

#### addBrand

CID.q.push(['**addBrand**', *brand*])

Chatbar will map `brand` to it's corresponding unique chat handle and add it to the Experts
List.

Configure CTAs
--------------

#### addCTA

CID.q.push(['**addCTA**', *cta*])

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

In the following example we append a CTA to some element with an ID of `chatid-cta`,
using dynamic text within the button:

```javascript
CID.q.push(['addCTA', {
  chatid: 'chatid.echo',
  container: 'chatid-cta',
  settings: {
    template: "<button class='chatid-cta'>Chat with <%= this.label %></button>"
  }
}]);
```

[View demo](https://s3.amazonaws.com/chatid-mojo/g/context/docs-cta/index.html)

Logging Events
--------------

#### log

CID.q.push(['**log**', *eventName*, *args...*])

`eventName` will be the key for which this unique behavior will be indexed. `args` may be
any number of additional arguments relevant to the event.

Here is an example using the `log` method to send Chatbar a conversion event:

```javascript
CID.q.push([
  'log', // 1st param is the API method, in this case it's 'log'
  'conversion', // 2nd param is first argument to the 'log' method, in this case it's 'conversion'
  [{ // 3rd param is the 2nd argument to the 'log' method, in this case, an array of products purchased
    brand: 'Acer',
    sku: '123456',
    name: 'Aspire A7',
    price: 349.99
  }, {
    brand: 'Seagate',
    sku: '654321',
    name: '500GB External HDD',
    price: 43.99
  }]
]);
```

If this snippet were to be placed on your site's confirmation page, ChatID would be able to associate the purchase with any chats this user may have participated in during his or her shopping experience.
