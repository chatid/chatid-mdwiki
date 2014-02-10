Public API Overview
===================

> [Home](index.md) ▸ [Public API](index.md#Public_API) ▸ **Overview**

For further documentation, please visit the [complete API reference](public-api-reference.md).

Basics
------

#### Async Syntax

*Adapted from [ga.js](https://developers.google.com/analytics/devguides/collection/gajs/)*

The `CID.q` object is what makes the asynchronous syntax possible. It acts as a queue,
which is a first-in, first-out data structure that collects API calls until Chatbar is
ready to execute them. To add something to the queue, use the `CID.q.push` method:

```javascript
CID.q.push(['<method>', args...])
```

The Experts List
----------------

The Experts List (also known as the Buddy List) is a panel within Chatbar that displays
the experts available for chat. Upon starting a chat, the expert will remain
in the List for the duration of the user's session.

![](./assets/screens/screen11.png "Experts List with just one ChatID (Acer)")

As a user browses your website, the List may update to display relevant experts. Chatbar
provides a few strategies for performing these updates.

If you know the unique string which identifies the expert, you may simply call `addChatId`. `chatid` may be just the string, or an object with a `chatid` field:

```javascript
CID.q.push(['addChatId', 'acer']);
// or
CID.q.push(['addChatId', { chatid: 'acer' }]);
```

Perhaps the simplest way to populate the Experts List from a retail website is to use the
`addProduct` method. Provide an object with a `brand` field, and ChatID will map that
`brand` string to the unique expert and add it to the List:

```javascript
CID.q.push(['addProduct', {
  brand: 'Acer',
  sku: 'AP123456',
  name: 'Aspire A7',
  price: 499.99
}]);
```

**NOTE:** brand mapping is only available *after* ChatID has configured your embed code and only for mapping ChatID-enabled brands.

*Reference*: [addChatId](public-api-reference.md#addChatId), [addProduct](public-api-reference.md#addProduct)

Configuring CTAs
----------------

Chatbar does not appear on your website until the user clicks a call to action (CTA). To
add CTAs to your page, use the `addCTA` API method:

```javascript
CID.q.push(['addCTA', {
  chatid: 'acer',
  container: '#chatid-cta-container',
  settings: {
    template: "<button class='chatid-cta'>Chat now</button>"
  }
}]);
```

*Reference*: [addCTA](public-api-reference.md#addCTA)
