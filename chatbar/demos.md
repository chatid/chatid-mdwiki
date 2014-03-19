Demos
=====

> [Home](index.md) ▸ [Examples](index.md#Examples) ▸ **Demos**

## Chat with Echo

In this example, we populate the Experts List with Echo the ChatID robot.

```
<div id='chatid-cta'></div>
<script>
CID.q.push(['addChatId', 'demo.chatid.echo']); // optional as `addCTA` will do this for us.
CID.q.push(['addCTA', {
  chatid: 'demo.chatid.echo',
  container: '#chatid-cta'
}]);
</script>
```

[View example](https://s3.amazonaws.com/chatid-mojo/g/context/docs-echo/index.html)

## Provide a dynamic template for the CTA

In this example, we generate the CTA message dynamically, referencing `this.label` from
the template string. The `template` field may be an EJS template for displaying the brand
name dynamically.

```
<div id='chatid-cta'></div>
<script>
CID.q.push(['addCTA', {
  chatid: 'demo.chatid.echo',
  container: '#chatid-cta',
  settings: {
    template: "<button data-ref='button'>Chat with <%= this.label %></button>"
  }
}]);
</script>
```

[View example](https://s3.amazonaws.com/chatid-mojo/g/context/docs-cta/index.html)

## Add experts by mapping a product to it's chatid

In this example, we populate the Experts List by mapping product data to it's `chatid`.
Then we add the chatid and corresponding CTA. Notice the use of a callback function for
getting the result of the first API call to accommodate async flow:

```
<div id='chatid-cta'></div>
<script>
CID.q.push(['mapProduct', {
  brand: 'iBUYPOWER',
  name: 'iBUYPOWER ARC Series NE611FX Desktop PC AMD FX-Series FX-4200 (3.3GHz) 4GB DDR3 1TB HDD Capacity Windows 8.1 64-Bit',
  merchant_sku: 'N82E16883227510',
  model: 'ARC Series NE611FX',
  price: '479.99',
  currency: 'USD',
  tags: ['PCs &amp; Laptops', 'Desktop PCs', 'All Desktop PCs', 'iBUYPOWER']
}, function(chatid) {
  CID.q.push(['addCTA', {
    chatid: chatid,
    container: '#chatid-cta',
    settings: {
      template: "Have product questions? <button data-ref='button'><img src='https://s3.amazonaws.com/chatid-mojo/g/assets/newegg/bubble-green.png' /> Chat with iBUYPOWER</button>"
    }
  }]);
}]);
</script>
```

[View example](https://s3.amazonaws.com/chatid-mojo/g/context/docs-map-product/index.html)
