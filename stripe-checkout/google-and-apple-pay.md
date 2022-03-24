---
description: Google Pay & Apple Pay are automatically supported by Stripe Checkout.
---

# Google & Apple Pay

No configuration or integration changes are required to enable Apple Pay or Google Pay in Stripe Checkout. These payments are handled the same way as other card payments.

## Google Pay

The Google Pay button is displayed in a given Checkout Session if all of the following apply:

* Google Pay is enabled for Checkout in your [Stripe Dashboard](https://dashboard.stripe.com/settings/checkout).
* The customer is using Google Chrome or Safari.
* The customer has a valid card registered with Google Pay.

This ensures that Checkout only displays the Google Pay button to customers who are able to use it.

Here's an example screenshot from Google Chrome running on Arch Linux, see the Google Pay button.

![Google Chrome running on Arch Linux](../.gitbook/assets/google-pay-demo.png)

## Apple Pay

The Apple Pay button is displayed in a given Checkout Session if all of the following apply:

* Apple Pay is enabled for Checkout in your [Stripe Dashboard](https://dashboard.stripe.com/settings/checkout).
* The customer’s device is running macOS 10.14.1+ or iOS 12.1+.
* The customer is using the Safari browser.
* The customer has a valid card registered with Apple Pay.

This ensures that Checkout only displays the Apple Pay button to customers who are able to use it.
