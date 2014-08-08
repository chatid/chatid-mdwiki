Retailer Implementation Instructions
====================================

ChatID is simple to deploy from any CMS or tag management tool. For assistance with your
particular system, please contact your Implementation Engineer and arrange an
implementation support call.

### Step 1: Global Tag

This tag should load on every page of your website.

    <script type='text/javascript'>
    (function(c,h,a,t,_,i,d){c[_]=c[_]||function(){
      (c[_].q=c[_].q||[]).push(arguments)},c[_].l=1*new Date();i=h.createElement(a),
      d=h.getElementsByTagName(a)[0];i.async=1;i.src=t;d.parentNode.insertBefore(i,d)
    })(window,document,'script','https://chatidcdn.com/chatbar/main/stable/1/main.js','CID');
    CID('initialize', 'example.qa');
    </script>
    <noscript><img src='https://ls.chatid.com/p.gif?data=%7B%22code%22%3A%22noscript%22%7D' width='1' height='1' /></noscript>

### Step 2: PDP Tag

In addition to the Global Tag, this tag should load on every product detail page and must
be configured with basic product metadata using your CMS or tag management tool.

    <script type='text/javascript'>
    (function(i,d){i[d]=i[d]||function(){(i[d].q=i[d].q||[]).push(arguments)};})(window,'CID');
    CID('page.setType', 'pdp', {
      brand: '{{ brand }}',               // (String) Product manufacturer's name
      name: '{{ product_name }}',         // (String) Product name
      merchant_sku: '{{ merchant_sku }}', // (String) Retailer-issued SKU or product identifier
      model: '{{ model }}',               // (String) Manufacturer-issued model number or product identifier
      unit_price: '{{ unit_price }}',     // (String) Original product price, without discounts applied
      sale_price: '{{ sale_price }}',     // (String) Same as unit_price if item is not on sale
      currency: '{{ currency }}',         // (String) i.e. 'USD'
      tags: {{ tags }}     // (Array) Tags/categories associated with the product
    });
    </script>

### Step 3: Conversion Tag

In addition to the Global Tag, this tag should load on the confirmation page and specify
basic product metadata for all items purchased.

    <script type=’text/javascript’>
    (function(i,d){i[d]=i[d]||function(){(i[d].q=i[d].q||[]).push(arguments)};})(window,'CID');
    CID('page.setType', 'receipt', [{
      brand: '{{ brand }}',               // (String) Product manufacturer's name
      name: '{{ product_name }}',         // (String) Product name
      merchant_sku: '{{ merchant_sku }}', // (String) Retailer-issued SKU or product identifier
      model: '{{ model }}',               // (String) Manufacturer-issued model number or product identifier
      quantity: {{ quantity }},           // (Integer) Quantity of this item purchased
      unit_price: '{{ unit_price }}',     // (String) Original product price, without discounts applied
      sale_price: '{{ sale_price }}',     // (String) Same as unit_price if item is not on sale
      currency: '{{ currency }}',         // (String) i.e. 'USD'
      tags: {{ tags }}     // (Array) Tags/categories associated with the product
    }, ... ]);
    </script>

### Step 4: Confirm Implementation

Your embed code has been pre-configured for testing purposes. To verify proper
installation, visit a product detail page and click to chat. Starting a chat will not
connect to the real vendor indicated, but instead to Echo the friendly ChatID robot.

FAQ
===

#### Does ChatID use any libraries that could conflict with existing code on our site?
All ChatID code is contained within a JavaScript closure, creating just one global (CID)
on the window object. CID defines the ChatID namespace and facilitates public API calls.

#### Can ChatID code block other tags from loading?
All ChatID code loads asynchronously and is served from chatidcdn.com, our dedicated
content delivery network.

#### How many round-trip requests does ChatID perform?
ChatID downloads two JS payloads, one sprite image, and runs two XHR calls per page load.
All static assets are cached for one hour.

#### Why does the Global Tag need to be loaded on all pages?
This is required to enable shoppers to start a chat on one page and continue chatting as
they browse. The interface will not appear until users click a call to action, and it may
be hidden or turned off from the settings menu.

#### How long does a user session last?
Users may close their browser after chatting and still return to view conversation history
for up to one hour. If they do not return for more than one hour, the ChatID interface
will be gone and conversation history lost, with all state reset as if starting from the
beginning.

#### Which browsers does this support?
ChatID supports IE7 and up along with Chrome, Safari, and Firefox on Mac/Windows/Linux for
desktop. Mobile support will arrive with Chatbar Mobile beginning Q4 2014. For
non-supported browsers, ChatID code immediately disables as if it had not been loaded at
all.
