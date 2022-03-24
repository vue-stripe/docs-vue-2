---
description: >-
  Vue Stripe is an easy to implement, and well maintained Vue.js plugin for
  Stripe Checkout, and Elements.
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

You just need to import your desired elements component wherever it is needed, and Stripe SDK will only be loaded by the time the component has been mounted.

```html
<template>
  <!-- stripe-element-card -->
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

