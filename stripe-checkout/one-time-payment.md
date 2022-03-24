---
description: Vue Stripe Checkout also supports one-time card payments.
---

# One-time Payment

## Demo

[Live Demo](https://vuestripe.com/stripe-checkout/one-time-payment)

## 1. Enable Checkout

You must first enable the client-only integration settings in your Stripe dashboard, you also have the option to customize the look and feel of your checkout page. [More details](https://stripe.com/docs/payments/checkout/client#enable-checkout).

## 2. Create products and prices

Product and Price are required to make this work. Whether it's a physical item or a service, it needs to be represented by a product. Each product can have one or more prices.

For example, you can create a T-shirt product, with different prices for different currencies. $20 USD and €15 Euro. [More details](https://stripe.com/docs/payments/checkout/client#create-products-and-prices).

## 3. Redirect to checkout

Follow the Vue Stripe Checkout example below:

```html
<template>
  <div>
    <stripe-checkout
      ref="checkoutRef"
      mode="payment"
      :pk="publishableKey"
      :line-items="lineItems"
      :success-url="successURL"
      :cancel-url="cancelURL"
      @loading="v => loading = v"
    />
    <button @click="submit">Pay now!</button>
  </div>
</template>

<script>
import { StripeCheckout } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeCheckout,
  },
  data () {
    this.publishableKey = process.env.STRIPE_PUBLISHABLE_KEY;
    return {
      loading: false,
      lineItems: [
        {
          price: 'some-price-id', // The id of the one-time price you created in your Stripe dashboard
          quantity: 1,
        },
      ],
      successURL: 'your-success-url',
      cancelURL: 'your-cancel-url',
    };
  },
  methods: {
    submit () {
      // You will be redirected to Stripe's secure checkout page
      this.$refs.checkoutRef.redirectToCheckout();
    },
  },
};
</script>
```
