Demos
=====

> [Home](index.md) ▸ [Examples](index.md#Examples) ▸ **Demos**

## Add experts by adding products

In this example, we populate the Experts List by mapping a brand string to it's `chatid`. Then we add the chatid and corresponding CTA. Notice the `template` field may be an EJS template to display the brand name dynamically.

```
<div id='chatid-cta'></div>
<script>
CID.q.push(['mapBrand', 'Acer', function(chatid) {
  CID.q.push(['addChatId', chatid]);
  CID.q.push(['addCTA', {
    chatid: chatid,
    container: '#chatid-cta',
    settings: {
      template: "<div data-ref='cta'><button class='chatid-cta' data-ref='button'>Chat with <%= this.label %></button></div>"
    }
  }]);
}]);
</script>
```

[View example](https://s3.amazonaws.com/chatid-mojo/g/context/docs-basic/index.html)
