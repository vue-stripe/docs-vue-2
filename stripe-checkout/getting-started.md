---
description: Vue Stripe Checkout starting guide.
---

# Getting Started

## Installation

{% tabs %}
{% tab title="Yarn" %}
{% code title="Terminal" %}
```bash
yarn add @vue-stripe/vue-stripe
```
{% endcode %}
{% endtab %}

{% tab title="NPM" %}
{% code title="Terminal" %}
```bash
npm install @vue-stripe/vue-stripe
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Usage



You just need to import the `StripeCheckout` component wherever it is needed and Stripe SDK will only be loaded by the time the component has been mounted.

```html
<template>
  <!-- stripe-checkout -->
</template>

<script>
import { StripeCheckout } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeCheckout,
  },
};
</script>
```

## Props

<table><thead><tr><th>Name</th><th>Type</th><th>Default</th><th data-type="select">Required</th><th>Description</th></tr></thead><tbody><tr><td>pk</td><td>string</td><td>none</td><td></td><td>Stripe's publishable key, you can retrieve this from your Stripe dashboard.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-sessionId">sessionId</a></td><td>string</td><td>none</td><td></td><td>The ID of the Checkout Session that is used in Checkout's client and server integration.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-lineItems">lineItems</a></td><td>array[object]</td><td>none</td><td></td><td>An array of objects representing the items that your customer would like to purchase. These items are shown as line items in the Checkout interface and make up the total amount to be collected by Checkout. Used with the client-only integration.</td></tr><tr><td><a href="https://stripe.com/docs/disputes/prevention/advanced-fraud-detection#disabling-advanced-fraud-detection">disableAdvancedFraudDetection</a></td><td>boolean</td><td>false</td><td></td><td>Disables the advanced fraud detection feature.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-mode">mode</a></td><td>string</td><td>none</td><td></td><td>The mode of the Checkout Session, one of <strong>payment</strong> or <strong>subscription</strong>. Required if using <strong>lineItems</strong> with the client-only integration.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-successUrl">successUrl</a></td><td>string</td><td>none</td><td></td><td>The URL to which Stripe should send customers when payment is complete. If you’d like access to the Checkout Session for the successful payment, read more about it in the guide on fulfilling orders. Required if using the client-only integration.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-cancelUrl">cancelUrl</a></td><td>string</td><td>none</td><td></td><td>The URL to which Stripe should send customers when payment is canceled. Required if using the client-only integration.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-clientReferenceId">clientReferenceId</a></td><td>string</td><td>none</td><td></td><td>A unique string to reference the Checkout session. This can be a customer ID, a cart ID, or similar. It is included in the checkout.session.completed webhook and can be used to fulfill the purchase.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-customerEmail">customerEmail</a></td><td>string</td><td>none</td><td></td><td>The email address used to create the customer object. If you already know your customer's email address, use this attribute to prefill it on Checkout.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-billingAddressCollection">billingAddressCollection</a></td><td>string</td><td>none</td><td></td><td>Specify whether Checkout should collect the customer’s billing address. If set to required, Checkout will attempt to collect the customer’s billing address. If not set or set to auto Checkout will only attempt to collect the billing address when necessary.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-shippingAddressCollection">shippingAddressCollection</a></td><td>object</td><td>none</td><td></td><td>When set, provides configuration for Checkout to collect a shipping address from a customer.</td></tr><tr><td><a href="https://stripe.com/docs/js/initializing#init_stripe_js-options-stripeAccount">stripeAccount</a></td><td>string</td><td>none</td><td></td><td>For usage with Connect only. Specifying a connected account ID (e.g., acct_24BFMpJ1svR5A89k) allows you to perform actions on behalf of that account.</td></tr><tr><td><a href="https://stripe.com/docs/js/initializing#init_stripe_js-options-apiVersion">apiVersion</a></td><td>string</td><td>none</td><td></td><td>Override your account's API version.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-locale">locale</a></td><td>string</td><td>none</td><td></td><td>Describes the type of transaction being performed by Checkout in order to customize relevant text on the page, such as the Submit button. submitType can only be specified when using using line items or SKUs, and not subscriptions. The default is auto. Supported values are: auto, book, donate, pay.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-submitType">submitType</a></td><td>string</td><td>auto</td><td></td><td>Describes the type of transaction being performed by Checkout in order to customize relevant text on the page, such as the Submit button. submitType can only be specified when using using line items or SKUs, and not subscriptions. The default is auto. Supported values are: auto, book, donate, pay.</td></tr><tr><td><a href="https://stripe.com/docs/js/checkout/redirect_to_checkout#stripe_checkout_redirect_to_checkout-options-items">items</a></td><td>array[object]</td><td>none</td><td></td><td>An array of objects representing the items that your customer would like to purchase. These items are shown as line items in the Checkout interface and make up the total amount to be collected by Checkout. Using lineItems is preferred.</td></tr></tbody></table>

## Events

| Name    | Type    | Description                                                                          |
| ------- | ------- | ------------------------------------------------------------------------------------ |
| loading | boolean | Emits the current loading state of the component.                                    |
| error   | object  | Emits whatever error the component might encounter, especially the ones from Stripe. |
