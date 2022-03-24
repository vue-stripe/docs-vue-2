---
description: Vue.js plugin for Stripe JS Object.
---

# 🔌 Vue Stripe Plugin

Maybe you don't need the checkout or the elements. Maybe you just need to access the other methods provided by the Stripe JS SDK. This plugin will help you do that.

## Step 1 - Import Stripe JavaScript SDK

{% tabs %}
{% tab title="HTML" %}
{% code title="index.html" %}
```html
<script src="https://js.stripe.com/v3"></script>
```
{% endcode %}
{% endtab %}

{% tab title="Nuxt" %}
{% code title="nuxt.config.js" %}
```javascript
export default {
  ...
  head: {
    script: [
      { src: 'https://js.stripe.com/v3' },
    ],
  },
  ...
};
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 2 - Install The Plugin

Import and register the `StripePlugin` plugin.

```javascript
import Vue from 'vue';
import { StripePlugin } from '@vue-stripe/vue-stripe';

const options = {
  pk: process.env.STRIPE_PUBLISHABLE_KEY,
  testMode: true, // Boolean. To override the insecure host warning
  stripeAccount: process.env.STRIPE_ACCOUNT,
  apiVersion: process.env.API_VERSION,
  locale: process.env.LOCALE,
};

Vue.use(StripePlugin, options);

```

This will give you access to `this.$stripe`, Where `this.$stripe` = `window.Stripe(PUBLISHABLE_KEY, options)`.

With this, you can now access the Stripe methods like, `.confirmCardPayment`, `.confirmAlipayPayment`, and more. See here.
