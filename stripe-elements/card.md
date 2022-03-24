---
description: The Card Element lets you collect card information all within one Element.
---

# Card

The Card Element lets you collect card information all within one Element. It includes a dynamically-updating card brand icon as well as inputs for number, expiry, CVC, and postal code. Get started with accepting payment.

## Demo

[Live Demo](https://vuestripe.com/stripe-elements/card)

## Usage

Import and register the `StripeElementCard` component.

```html
<template>
  <div>
    <stripe-element-card/>
  </div>
</template>

<script>
import { StripeElementCard } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeElementCard,
  },
};
</script>
```

## Example

Below is an example of how to use `StripeElementCard` to generate a token.

```html
<template>
  <div>
    <stripe-element-card
      ref="elementRef"
      :pk="publishableKey"
      @token="tokenCreated"
    />
    <button @click="submit">Generate token</button>
  </div>
</template>

<script>
import { StripeElementCard } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeElementCard,
  },
  data () {
    this.publishableKey = process.env.STRIPE_PUBLISHABLE_KEY;
    return {
      token: null,
    };
  },
  methods: {
    submit () {
      // this will trigger the process
      this.$refs.elementRef.submit();
    },
    tokenCreated (token) {
      console.log(token);
      // handle the token
      // send it to your server
    },
  }
};
</script>
```

## Props

<table><thead><tr><th>Name</th><th>Type</th><th>Default</th><th data-type="select">Required</th><th>Description</th></tr></thead><tbody><tr><td>pk</td><td>string</td><td>none</td><td></td><td>Stripe's publishable key, you can retrieve this from your Stripe dashboard.</td></tr><tr><td>testMode</td><td>boolean</td><td>false</td><td></td><td>Add this if you want to bypass the insecure host warning when testing to a non-localhost or non-https links.</td></tr><tr><td><a href="https://stripe.com/docs/js/elements_object/create#stripe_elements-options">elementsOptions</a></td><td>object</td><td>none</td><td></td><td>A set of options to create this Elements instance with.</td></tr><tr><td><a href="https://stripe.com/docs/js/tokens_sources/create_token?type=cardElement">tokenData</a></td><td>object</td><td>none</td><td></td><td>An object containing additional payment information you might have collected. Although these fields are optional, we highly recommend collecting name and address.</td></tr><tr><td><a href="https://stripe.com/docs/disputes/prevention/advanced-fraud-detection#disabling-advanced-fraud-detection">disableAdvancedFraudDetection</a></td><td>boolean</td><td>false</td><td></td><td>Disables the advanced fraud detection feature.</td></tr><tr><td><a href="https://stripe.com/docs/js/elements_object/create_element?type=card#elements_create-options-classes">classes</a></td><td>object</td><td>none</td><td></td><td>Set custom class names on the container DOM element when the Stripe element is in a particular state.</td></tr><tr><td><a href="https://stripe.com/docs/js/elements_object/create_element?type=card#elements_create-options-style">elementStyle</a></td><td>object</td><td>none</td><td></td><td>Customize the appearance of this element using CSS properties passed in a Style object.</td></tr><tr><td><a href="https://stripe.com/docs/js/elements_object/create_element?type=card#elements_create-options-value">value</a></td><td>string</td><td>none</td><td></td><td>A pre-filled set of values to include in the input (e.g., <code>{postalCode: '94110'}</code>). Note that sensitive card information (card number, CVC, and expiration date) cannot be pre-filled.</td></tr><tr><td><a href="https://stripe.com/docs/js/elements_object/create_element?type=card#elements_create-options-hidePostalCode">hidePostalCode</a></td><td>boolean</td><td>false</td><td></td><td>Hide the postal code field. Default is false. If you are already collecting a full billing address or postal code elsewhere, set this to true.</td></tr><tr><td><a href="https://stripe.com/docs/js/elements_object/create_element?type=card#elements_create-options-iconStyle">iconStyle</a></td><td>string</td><td>default</td><td></td><td>Appearance of the icon in the Element. Either solid or default.</td></tr><tr><td><a href="https://stripe.com/docs/js/elements_object/create_element?type=card#elements_create-options-hideIcon">hideIcon</a></td><td>boolean</td><td>none</td><td></td><td>Hides the icon in the Element. Default is false.</td></tr><tr><td><a href="https://stripe.com/docs/js/elements_object/create_element?type=card#elements_create-options-disabled">disabled</a></td><td>boolean</td><td>none</td><td></td><td>Applies a disabled state to the Element such that user input is not accepted. Default is false.</td></tr><tr><td><a href="https://stripe.com/docs/js/initializing#init_stripe_js-options-stripeAccount">stripeAccount</a></td><td>string</td><td>none</td><td></td><td>For usage with Connect only. Specifying a connected account ID (e.g., acct_24BFMpJ1svR5A89k) allows you to perform actions on behalf of that account.</td></tr><tr><td><a href="https://stripe.com/docs/js/initializing#init_stripe_js-options-apiVersion">apiVersion</a></td><td>string</td><td>none</td><td></td><td>Override your account's API version.</td></tr><tr><td><a href="https://stripe.com/docs/js/initializing#init_stripe_js-options-locale">locale</a></td><td>string</td><td>auto</td><td></td><td><p>A locale used to globally configure localization in Stripe. Setting the locale here will localize error strings for all Stripe.js methods. It will also configure the locale for Elements and Checkout. Default is auto (Stripe detects the locale of the browser).</p><p>Note that Checkout supports a slightly different set of locales than Stripe.js.</p></td></tr></tbody></table>

## Methods

You can access these methods via `$refs`, like so `this.$refs.elementRef.destroy()`.

| Name                                                                           | Return Type | Description                                                                                                             |
| ------------------------------------------------------------------------------ | ----------- | ----------------------------------------------------------------------------------------------------------------------- |
| blur()                                                                         | void        | Blurs the Element.                                                                                                      |
| clear()                                                                        | void        | Clears the value(s) of the Element.                                                                                     |
| destroy()                                                                      | void        | Removes the Element from the DOM and destroys it. A destroyed Element can not be re-activated or re-mounted to the DOM. |
| focus()                                                                        | void        | Focuses the Element.                                                                                                    |
| unmount()                                                                      | void        | Unmounts the Element from the DOM. Call element.mount to re-attach it to the DOM.                                       |
| [update()](https://stripe.com/docs/js/element/other\_methods/update?type=card) | void        | Updates the options the Element was initialized with. Updates are merged into the existing configuration.               |

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
