---
title: Stripe Payment Plugin
---

The Stripe payment plugin allows you to handle payments through your [Stripe](https://stripe.com/) account. If you don’t already have a Stripe account, you can create one for free and use the test credentials they provide to try this plugin without creating actual charges.

The Stripe client components all communicate directly with Stripe servers and create secure tokens. This ensures that no sensitive financial details are ever sent to your servers, which is part of having a [PCI-compliant](https://stripe.com/docs/security#pci-dss-guidelines) system. This does not mean that there is zero risk; the source tokens are still sent to your servers, and they each can be used to create a single charge of any amount, if your Stripe secret key is compromised.

## Payment Methods

### Stripe Card
The "Stripe Card" payment method, which is provided by this plugin, allows a shopper to enter credit card details as payment for an order. Users in the United States can accept Visa, Mastercard, American Express, Discover, JCB, Diners Club, and China UnionPay credit and debit cards. The exact cards that are supported varies by country. Refer to [Stripe documentation](https://stripe.com/docs/sources/cards) for more details.

## How to: Enable and Configure Stripe Payments

> Prerequisite: Create a free Stripe account. A test account is enough if you are only testing or developing.

### Plugin Configuration

1. Log in to `reaction-admin` (on [localhost:4080](http://localhost:4080) if you're running it locally) with an account that has permission to access plugin settings.
2. In the sidebar, go to Settings > Payment.
3. You should see a section with a toggle for each payment plugin. If it is not already enabled, click the toggle to enable the Stripe plugin.
4. With the Stripe payment method enabled, head to your API's environment variables (in `<PROJECT_ROOT>/reaction/.env` if you're running it locally) and set `STRIPE_API_KEY` to your Stripe Secret Key. Copy it from your Stripe account. The Secret Key begins with `sk_`. If you are using a development or testing environment, be sure to use the “test” keys so that you can enter fake credit card details and no money will actually change hands.

This is the only server configuration necessary.

### Client Components

If you are using the `example-storefront` provided by Reaction, the necessary client components are already included and will appear where they should. If you are building your own client, you may want to use our [StripeForm React component](https://designsystem.reactioncommerce.com/#!/StripeForm), which is part of the Example Storefront Component Library. It wraps [react-stripe-elements](https://github.com/stripe/react-stripe-elements) to do some of the work for you, but you can also use `react-stripe-elements` directly, or use any Stripe client that allows you to securely create a source token.

> For Stripe payments to work in `example-storefront`, you must set the `STRIPE_PUBLIC_API_KEY` environment variable to your Publishable Key (beginning with `pk_`). This is done in `<PROJECT_ROOT>/example-storefront/.env` for local environments.


## How to: Test a Stripe Payment

> Prerequisite: Enable and configure Stripe payments with "test" keys

1. Access the storefront UI (on [localhost:4000](http://localhost:4000) if you're running it locally).
2. Add items to your cart and begin checkout.
3. When you get to the payment step, choose "Credit Card" payment method if multiple options are shown.
4. You should see the Stripe credit card entry form. Enter the following test information in the fields:
    - One of Stripe’s [test card numbers](https://stripe.com/docs/testing#cards), such as 4242 4242 4242 4242
    - Any three-digit CVC code
    - Any expiration date in the future
    - Any billing ZIP code, such as 12345
