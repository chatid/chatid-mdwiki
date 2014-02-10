Implementation
==============

> [Home](index.md) ▸ [Overview](index.md#Overview) ▸ **Implementation**

To get started, add your Chatbar embed code to all pages. Your embed code looks like the following, with `example.js` swapped for your company's identifier:

```
<script type='text/javascript'>
var CID = (CID && CID.q) ? CID : { q: [] };
(function(d) {
  var cid = d.createElement('script'); cid.type = 'text/javascript'; cid.async = true;
  cid.src = 'https://s3.amazonaws.com/chatid-mojo/g/config/example.js';
  var s = d.getElementsByTagName('script')[0]; s.parentNode.insertBefore(cid, s);
})(document);
</script>
<noscript><img src='https://ls.chatid.com/p.gif?data=%7B%22code%22%3A%22noscript%22%7D' width='1' height='1' /></noscript>
```

While Chatbar does not display by default, the JavaScript must be available across your website to ensure seamless chatting page to page.

After adding your Chatbar embed code to all pages, there are just 2 additional steps before it's ready:

* Add calls to action (CTAs)
* Populate the Experts List

Both can be accomplished using Chatbar's [public API](public-api-overview.md). Add the following API calls so you may begin chatting with the Echo, the friendly ChatID Robot:

```javascript
CID.q.push(['addChatId', 'chatid.echo']);
CID.q.push(['addCTA', {
  chatid: 'chatid.echo',
  container: '#chatid-cta',
  settings: {
    template: "<button data-ref='button'>Chat with Echo</button>"
  }
}]);
```

And then add an HTML container with an id of `chatid-cta`:

```
<div id='chatid-cta'></div>
```

And that's it! Open the HTML page and fire off a test chat, it should appear similar to [this demo](https://s3.amazonaws.com/chatid-mojo/g/context/docs-echo/index.html).

**NOTE:** The HTML page must be served by a webserver for chat to work properly. For debugging, try the node.js npm module, `http-server` or `python -m SimpleHTTPServer`.

#### Next

* Browse [Examples](demos.md)
* Read the [API Overview](public-api-overview.md)
* Explore the [API Reference](public-api-reference.md)
