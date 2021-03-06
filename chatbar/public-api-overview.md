Public API Overview
===================

> [Chatbar](index.md) ▸ [Public API](index.md#Public_API) ▸ **Overview**

For further documentation, please visit the
[complete API reference](public-api-reference.md).

Basics
------

#### Asynchronous Loading

*Adapted from [ga.js](https://developers.google.com/analytics/devguides/collection/gajs/)*

The `CID` object is your interface for asynchornously calling the Chatbar public API.
It acts as a queue, which is a first-in, first-out data structure that collects API calls
until Chatbar is ready to execute them. To add something to the queue, call `CID` with the
method name as the first argument:

```javascript
CID('<method>', args...)
```

#### Where to place API calls

Calls to the Public API should be placed directly after your embed code, following the
first call to "initialize", and no earlier:

```
<script type='text/javascript'>
(function(c,h,a,t,_,i,d){c[_]=c[_]||function(){
  (c[_].q=c[_].q||[]).push(arguments)},c[_].l=1*new Date();i=h.createElement(a),
  d=h.getElementsByTagName(a)[0];i.async=1;i.src=t;d.parentNode.insertBefore(i,d)
})(window,document,'script','//chatidcdn.com/chatbar/main/stable/1/main.js','CID');
CID('initialize', 'demo.chatbar');
// Now make API calls here
CID('chatids.add', 'demo.chatid.echo');
</script>
<noscript><img src='https://ls.chatid.com/p.gif?data=%7B%22code%22%3A%22noscript%22%7D' width='1' height='1' /></noscript>
```

The Experts List
----------------

The Experts List (also known as the Buddy List) is a panel within Chatbar that displays
the experts available for chat. Upon starting a chat, the expert will remain in the List
for the duration of the user's session, with a clock icon to indicate chat history:

![](./assets/screens/screen11.png "Experts List with just one ChatID (Acer)")

As a user browses your website, the List may update to display relevant experts. Chatbar
provides a few strategies for performing these updates.

If you know the unique string which identifies the expert, you may simply call `chatids.add`
and pass it as the first argument:

```javascript
CID('chatids.add', 'acer');
```

*Reference*: [chatids.add](public-api-reference.md#chatids.add)

Configuring CTAs
----------------

Chatbar does not appear on your website until the user clicks a call to action (CTA). To
add CTAs to your page, use the `ctas.insert` API method:

```javascript
CID('ctas.insert', {
  chatid: 'acer',
  container: '#chatid-cta',
  settings: {
    template: "<button data-ref='button'>Chat now</button>"
  }
});
```

`ctas.insert` will call `chatids.add` internally if you haven't done so already.

*Reference*: [ctas.insert](public-api-reference.md#ctas.insert)

**NOTE:** CTAs will not display unless experts are online and available for chat.
Currently, there is no mechanism for checking expert availability via the public API, so
all configuration should be done with the awareness that CTAs tied to unavailable chatids
will simply not appear.

#### Next

* Dig deeper with the [API Reference](public-api-reference.md)
* Browse [Examples](demos.md)
