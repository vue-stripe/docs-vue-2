---
description: Easy to implement custom payment elements by Stripe.
---

# Payment

## Demo

[Live Demo](https://vuestripe.com/stripe-elements/payment)

## 1. Generate ClientSecret <mark style="color:blue;background-color:red;">\[backend]</mark>

ClientSecret is required to render the Payment UI. You first have to generate one by creating a PaymentIntent. See how [here](https://stripe.com/docs/api/payment\_intents/create?lang=node).

The ClientSecret looks like this `pi_3KIBJd...MLhhr1DIBc5qg_secret_skk...3HIXCXtGjDA`

## 2. Render Payment UI <mark style="color:green;background-color:blue;">\[frontend]</mark>

Import the component like so:

```html
<template>
  <!-- stripe-element-payment -->
</template>

<script>
import { StripeElementPayment } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeElementPayment,
  },
};
</script>
```

Full code example:

```html
<template>
  <div>
    <stripe-element-payment
      ref="paymentRef"
      :pk="pk"
      :elements-options="elementsOptions"
      :confirm-params="confirmParams"
    />
    <button @click="pay">Pay Now</button>
  </div>
</template>

<script>
import { StripeElementPayment } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeElementPayment,
  },
  data () {
    return {
      pk: 'your-publishable-key',
      elementsOptions: {
        appearance: {}, // appearance options
      },
      confirmParams: {
        return_url: 'http://localhost:8080/success', // success url
      },
    };
  },
  mounted () {
    this.generatePaymentIntent();
  },
  methods: {
    async generatePaymentIntent () {
      const paymentIntent = await apiCallToGeneratePaymentIntent(); // this is just a dummy, create your own API call
      this.elementsOptions.clientSecret = paymentIntent.client_secret;
    }
    pay () {
      this.$refs.paymentRef.submit();
    },
  },
};
</script>
```

For a more comprehensive tutorial, go here [https://stripe.com/docs/payments/quickstart](https://stripe.com/docs/payments/quickstart)

## Props

<table><thead><tr><th>Name</th><th>Type</th><th>Default</th><th data-type="select">Required</th><th>Description</th></tr></thead><tbody><tr><td>pk</td><td>string</td><td>none</td><td></td><td>Stripe's publishable key, you can retrieve this from your Stripe dashboard.</td></tr><tr><td>testMode</td><td>boolean</td><td>false</td><td></td><td>Add this if you want to bypass the insecure host warning when testing to a non-localhost or non-https links.</td></tr><tr><td><a href="https://stripe.com/docs/js/elements_object/create#stripe_elements-options">elementsOptions</a></td><td>Object</td><td>none</td><td></td><td>A set of options to create this Elements instance with.</td></tr><tr><td><a href="https://stripe.com/docs/js/payment_intents/confirm_payment">confirmParams</a></td><td>Object</td><td>none</td><td></td><td>A set of options to confirm a PaymentIntent.</td></tr><tr><td><a href="https://stripe.com/docs/js/initializing#init_stripe_js-options-stripeAccount">stripeAccount</a></td><td>string</td><td>none</td><td></td><td>For usage with Connect only. Specifying a connected account ID (e.g., acct_24BFMpJ1svR5A89k) allows you to perform actions on behalf of that account.</td></tr><tr><td><a href="https://stripe.com/docs/js/initializing#init_stripe_js-options-apiVersion">apiVersion</a></td><td>string</td><td>none</td><td></td><td>Override your account's API version.</td></tr><tr><td><a href="https://stripe.com/docs/js/initializing#init_stripe_js-options-locale">locale</a></td><td>string</td><td>none</td><td></td><td><p>A locale used to globally configure localization in Stripe. Setting the locale here will localize error strings for all Stripe.js methods. It will also configure the locale for Elements and Checkout. Default is auto (Stripe detects the locale of the browser).</p><p>Note that Checkout supports a slightly different set of locales than Stripe.js.</p></td></tr><tr><td><a href="https://stripe.com/docs/disputes/prevention/advanced-fraud-detection#disabling-advanced-fraud-detection">disableAdvancedFraudDetection</a></td><td>boolean</td><td>false</td><td></td><td>Disables the advanced fraud detection feature.</td></tr></tbody></table>

## Methods

| Name         | Return Type | Description                                                                                                                             |
| ------------ | ----------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| submit()     | void        | Submits the payment                                                                                                                     |
| clear()      | void        | Clears the value(s) of the Element.                                                                                                     |
| destroy()    | void        | Removes the Element from the DOM and destroys it. A destroyed Element can not be re-activated or re-mounted to the DOM.                 |
| focus()      | void        | Focuses the Element.                                                                                                                    |
| unmount()    | void        | Unmounts the Element from the DOM. Call element.mount to re-attach it to the DOM.                                                       |
| collapse()   | void        | Collapses the Payment Element into a row of payment method tabs                                                                         |
| getElement() | Object      | Retrieves a previously created element                                                                                                  |
| update()     | void        | Updates the element. See official docs for more detail: https://site-admin.stripe.com/docs/js/elements\_object/update\_payment\_element |

## Events

| Name           | Return Type | Description                                                                                                                                                |
| -------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| token          | object      | Emits the card source or the tokenized version of the user's card                                                                                          |
| loading        | boolean     | Emits the current loading state of the component.                                                                                                          |
| error          | object      | Emits whatever error the component might encounter, especially the ones from Stripe.                                                                       |
| element-change | void        | The change event is triggered when the Element's value changes. The event payload always contains certain keys, in addition to some Element-specific keys. |
| element-ready  | void        | Triggered when the Element is fully rendered and can accept element.focus calls.                                                                           |
| element-focus  | void        | Triggered when the Element gains focus.                                                                                                                    |
| element-blur   | void        | Triggered when the Element loses focus.                                                                                                                    |
| element-escape | void        | Triggered when the escape key is pressed within an Element.                                                                                                |
| element-click  | void        | Triggered when the Element is clicked. This event is only emmited from a paymentRequestButton Element.                                                     |
