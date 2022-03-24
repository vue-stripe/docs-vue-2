---
description: This is just one use-case of Vue Stripe Plugin.
---

# Separate Card Fields

## Demo

[Live Demo](https://vuestripe.com/stripe-elements/separate-card-fields)

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

## Step 2 - Install Vue Stripe Plugin

Import and register the `StripePlugin` plugin.

```javascript
import Vue from 'vue';
import { StripePlugin } from '@vue-stripe/vue-stripe';

const options = {
  pk: process.env.STRIPE_PUBLISHABLE_KEY,
  stripeAccount: process.env.STRIPE_ACCOUNT,
  apiVersion: process.env.API_VERSION,
  locale: process.env.LOCALE,
};

Vue.use(StripePlugin, options);
```

This will give you access to `this.$stripe`. Using this you can create now create an instance of Stripe Elements.

With this, you can now access the Elements methods like, `.create`, `.getElement`, and more. See here.

## Step 3 - Use Case

Separate components for each card field.

Official components for these are still in development. So this is just a sample to help you implement them on your own.

```html
<template>
  <div>
    <label>Card Number</label>
    <div id="card-number"></div>
    <label>Card Expiry</label>
    <div id="card-expiry"></div>
    <label>Card CVC</label>
    <div id="card-cvc"></div>
    <div id="card-error"></div>
    <button id="custom-button" @click="createToken">Generate Token</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      token: null,
      cardNumber: null,
      cardExpiry: null,
      cardCvc: null,
    };
  },
  computed: {
    stripeElements () {
      return this.$stripe.elements();
    },
  },
  mounted () {
    // Style Object documentation here: https://stripe.com/docs/js/appendix/style
    const style = {
      base: {
        color: 'black',
        fontFamily: '"Helvetica Neue", Helvetica, sans-serif',
        fontSmoothing: 'antialiased',
        fontSize: '14px',
        '::placeholder': {
          color: '#aab7c4',
        },
      },
      invalid: {
        color: '#fa755a',
        iconColor: '#fa755a',
      },
    };
    this.cardNumber = this.stripeElements.create('cardNumber', { style });
    this.cardNumber.mount('#card-number');
    this.cardExpiry = this.stripeElements.create('cardExpiry', { style });
    this.cardExpiry.mount('#card-expiry');
    this.cardCvc = this.stripeElements.create('cardCvc', { style });
    this.cardCvc.mount('#card-cvc');
  },
  beforeDestroy () {
    this.cardNumber.destroy();
    this.cardExpiry.destroy();
    this.cardCvc.destroy();
  },
  methods: {
    async createToken () {
      const { token, error } = await this.$stripe.createToken(this.cardNumber);
      if (error) {
        // handle error here
        document.getElementById('card-error').innerHTML = error.message;
        return;
      }
      console.log(token);
      // handle the token
      // send it to your server
    },
  }
};
</script>

<style scoped>
#custom-button {
  height: 30px;
  outline: 1px solid grey;
  background-color: green;
  padding: 5px;
  color: white;
}

#card-error {
  color: red;
}
</style>
```
