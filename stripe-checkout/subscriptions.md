---
description: Vue Stripe Checkout also supports subscription or recurring payments.
---

# Subscriptions

## Demo

[Live Demo](https://vuestripe.com/stripe-checkout/recurring-payment)

## 1. Enable Checkout

You must first enable the client-only integration settings in your Stripe dashboard, you also have the option to customize the look and feel of your checkout page. [More details](https://stripe.com/docs/payments/checkout/client-subscription#enable-checkout).

## 2. Create products and recurring prices

Product and Price are required to make this work. Whether it's a physical item or a service, it needs to be represented by a product. Each product can have one or more prices.

For example, you can create a software product with different subscription tiers. $10/month, $20/month, and $50/month [More details](https://stripe.com/docs/payments/checkout/client-subscription#create-products-and-prices).

## 3. Redirect to checkout

Follow the Vue Stripe Checkout example below:

```html
<template>
  <div>
    <stripe-checkout
      ref="checkoutRef"
      mode="subscription"
      :pk="publishableKey"
      :line-items="lineItems"
      :success-url="successURL"
      :cancel-url="cancelURL"
      @loading="v => loading = v"
    />
    <button @click="submit">Subscribe!</button>
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
          price: 'some-price-id', // The id of the recurring price you created in your Stripe dashboard
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
