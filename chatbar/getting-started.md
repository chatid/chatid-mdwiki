Getting Started
===============

> [Home](index.md) ▸ [Overview](index.md#Overview) ▸ **Getting Started**

To get started, add your Chatbar embed code to all pages. Your embed code looks like the
following, with `demo.chatbar` swapped for your client's identifier (usually your
company's name):

```
<!-- ChatID Chatbar -->
<script type='text/javascript'>
(function(c,h,a,t,_,i,d){c[_]=c[_]||function(){
  (c[_].q=c[_].q||[]).push(arguments)},c[_].l=1*new Date();i=h.createElement(a),
  d=h.getElementsByTagName(a)[0];i.async=1;i.src=t;d.parentNode.insertBefore(i,d)
})(window,document,'script','//chatidcdn.com/chatbar/main/stable/1/main.js','CID');
CID('initialize', { channelName: 'demo.chatbar' });
</script>
<noscript><img src='https://ls.chatid.com/p.gif?data=%7B%22code%22%3A%22noscript%22%7D' width='1' height='1' /></noscript>
<!-- End ChatID Chatbar -->
```

While Chatbar does not display by default, the JavaScript must be available across your
website to ensure seamless chatting page to page.

After adding your Chatbar embed code to all pages, there are just 2 additional steps
before it's ready:

* Add calls to action (CTAs)
* Populate the Experts List

Both can be accomplished using Chatbar's [public API](public-api-overview.md). Add the
following API call so you can chat with Echo, the friendly ChatID robot:

```javascript
CID('addCTA', {
  chatid: 'demo.chatid.echo',
  container: '#chatid-cta'
});
```

And then add an HTML container with an `id` of `chatid-cta`:

```
<div id='chatid-cta'></div>
```

That's it! Open the HTML page and fire off a test chat. You should see something similar
to [this demo](http://demo.chatid.com/chatbar/docs-echo/index.html).

**HINT:** The HTML page must be served by a webserver for chat to work properly. For
debugging, try the node.js npm module, `http-server` or `python -m SimpleHTTPServer`.

**NOTE:** While Echo the robot is available for chat 24/7, experts in the ChatID Network
may occasionally go offline, which will cause their CTAs to become hidden. To further
understand how Chatbar handles availability, visit
[Configuring CTAs](public-api-overview.md#Configuring_CTAs).

#### Next

* Read the [API Overview](public-api-overview.md)
* Are you a retailer? [Retailer Implementation Guide](retailer-implementation.md)
* Explore the [API Reference](public-api-reference.md)
* Browse [Examples](demos.md)
