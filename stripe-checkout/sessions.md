---
description: Vue Stripe Checkout also supports checkout using Session Id.
---

# Sessions

Take note that `Session` ids are generated from the backend. To know more about sessions visit the [documentation](https://stripe.com/docs/api/checkout/sessions).

## 1. Create a session

You need to create the session in your backend. This session will return an `id`, use that id to checkout the payment.

## 2. Redirect to checkout

Follow the Vue Stripe Checkout example below:

You'll notice that when using sessions, you'll only need the `session-id`. This is because the session is the representation of all of the information (including success, and cancel URLs) about the payment to be done.

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
