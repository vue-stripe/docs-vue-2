---
description: Interactive session generator to demo checkout using sessions.
---

# Sessions Generator

Take note that `Session` ids are generated from the backend. To know more about sessions visit the documentation.

## Demo

[Session Generator Demo](https://vuestripe.com/stripe-checkout/sessions-generator)

## 1. Prepare checkout data <mark style="color:green;background-color:blue;">\[frontend]</mark>

Prerequisite: [Enable Checkout, and Create Products](https://vuestripe.com/stripe-checkout/one-time-payment)

```json
{
  "success_url": "https://vuestripe.com/stripe-checkout/sessions-generator?state=success",
  "cancel_url": "https://vuestripe.com/stripe-checkout/sessions-generator?state=cancel",
  "payment_method_types": [
    "card"
  ],
  "line_items": [
    {
      "price": "price_1I1xv3EfCmJMLhhrJ5vdGxy6",
      "quantity": 1
    }
  ],
  "mode": "payment"
}
```

## 2. Create a Session <mark style="color:blue;background-color:red;">\[backend]</mark>

Create a session using the data from Step 1. Note that the `"mode"="payment"` means that you are creating a one-time payment session. [Node.js sample here](https://github.com/vue-stripe/vue-stripe-functions).

## 3. Checkout using Session id <mark style="color:green;background-color:blue;">\[frontend]</mark>

Follow this sample code below:

```html
<template>
  <div>
    <stripe-checkout
      ref="checkoutRef"
      :pk="publishableKey"
      :session-id="sessionId"
    />
    <button @click="submit">Checkout!</button>
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
      sessionId: 'session-id', // session id from backend
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
