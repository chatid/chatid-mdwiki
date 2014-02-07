Public API Reference
====================

> [Home](index.md) ▸ [Public API](public-api-overview.md) ▸ **Reference**

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

* `chatid` must be the unique string with which this CTA is connected.
* `container` may be a DOM element or a jQuery selector string.
* `settings` should be an object with a `template` field.
* `template` must be a string of HTML to inject within `container`. It may also be a
JavaScript template for use with [_.template](http://underscorejs.org/#template). It
will be rendered with the following metadata for its context:

```javascript
{
  active: false,
  available: true,
  label: 'Acer',
  channel: false
}
```

In the following example we append a CTA some element with `product-details` for its ID,
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


Event Logging
-------------

#### hookEvents

CID.q.push(['**hookEvents**', *customLogger*]

Capture Chatbar events.

`customLogger` must be an object with a `codeMap` object and a `trackEvent` method.
Here is an example `customLogger` hooking events for Google Analytics:

```javascript
CID.q.push(['hookEvents', {
  codeMap: {
    'cta_click': 'chatid_cta_click'
  },
  trackEvent: function(options) {
    data = data || {};
    var code = data.code, csid = data.csid;
    if (code && csid) _gaq.push(['_trackEvent', this.codeMap[code], csid]);
  }
}]);
```
