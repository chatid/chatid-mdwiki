Demos
=====

> [Chatbar](index.md) ▸ [Examples](index.md#Examples) ▸ **Demos**

## Chat with Echo

In this example, we populate the Experts List with Echo the ChatID robot.

```
<div id='chatid-cta'></div>
<script>
CID('chatids.add', 'demo.chatid.echo'); // optional as `ctas.insert` will do this for us.
CID('ctas.insert', {
  chatid: 'demo.chatid.echo',
  container: '#chatid-cta'
});
</script>
```

[View example](http://demo.chatid.com/chatbar/docs-echo/index.html)

## Provide a dynamic template for the CTA

In this example, we generate the CTA message dynamically, referencing `this.label` from
the template string. The `template` field may be an EJS template for displaying the brand
name dynamically.

```
<div id='chatid-cta'></div>
<script>
CID('ctas.insert', {
  chatid: 'demo.chatid.echo',
  container: '#chatid-cta',
  settings: {
    template: "<button data-ref='button'>Chat with <%= this.label %></button>"
  }
});
</script>
```

[View example](http://demo.chatid.com/chatbar/docs-cta/index.html)

## Add experts by mapping a brand to it's chatid

In this example, we populate the Experts List by mapping a brand name to it's `chatid`.
Then we add the chatid and corresponding CTA. Notice the use of a callback function for
getting the result of the first API call to accommodate async flow:

```
<div id='chatid-cta'></div>
<script>
CID('chatids.lookup.byBrand', 'iBUYPOWER', function(chatid) {
  CID('ctas.insert', {
    chatid: chatid,
    container: '#chatid-cta',
    settings: {
      template: "Have product questions? <button data-ref='button'><img src='https://s3.amazonaws.com/chatid-mojo/g/assets/newegg/bubble-green.png' /> Chat with iBUYPOWER</button>"
    }
  });
});
</script>
```

[View example](http://demo.chatid.com/chatbar/docs-map-brand/index.html)
