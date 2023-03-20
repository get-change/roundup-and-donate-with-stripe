# Round up and donate

Round up and donate features are used in checkout flows to raise money for an organization or nonprofit the business wants to support. It's easy to create your own round up and donate feature using [Change](https://getchange.io/) and [Stripe](https://stripe.com/).

If you'd rather see this demo in a guide format, [look here](https://docs.getchange.io/recipes/roundup-and-donate-with-stripe/).

## How to run locally

First, clone this repo:

```
git clone git@github.com:get-change/roundup-and-donate-with-stripe.git
```

Copy the .env.example file into a file named .env in the `server` folder:

```
cp .env.example server/.env
```

You will need a Change account in order to run the demo. [Sign up](https://api.getchange.io/merchants/sign_up) to receive a set of test API keys.

Once you sign up, add your API keys to `server/.env`:

```
CHANGE_PUBLIC_KEY=<replace-with-your-public-key>
CHANGE_SECRET_KEY=<replace-with-your-secret-key>
```

You will also need a Stripe account in order to run the demo. Once you set up your account, go to the Stripe [developer dashboard](https://stripe.com/docs/development/quickstart#api-keys) to find your API keys.

Make sure you use your test keys (they start with `pk_test` and `sk_test`).

```
STRIPE_PUBLISHABLE_KEY=<replace-with-your-publishable-key>
STRIPE_SECRET_KEY=<replace-with-your-secret-key>
```

This demo utilizes Stripe webhooks. Stripe makes it simple to test their webhooks using the Stripe CLI. Get the Stripe CLI using Homebrew (for other installation methods, see this [Stripe doc](https://stripe.com/docs/webhooks/test)).

```
brew install stripe/stripe-cli/stripe
```

Login to the Stripe CLI:

```
stripe login
```

Tell Stripe to forward webhooks to the server we're about to run:

```
stripe listen --forward-to localhost:4242/webhook
```

It should print your webhook secret. Grab that secret and put it in `server/.env`:

```
STRIPE_WEBHOOK_SECRET=<replace-with-your-webhook-secret>
```

Now we're ready to start the server. To start the server, run:

```
cd server
bundle install
ruby server.rb
```

Visit your browser at localhost:4242. Enter the card number `4242 4242 4242 4242` with any CVV and future date. Click "Round up and donate", then click "Pay".

Congrats!

Check the server logs. You should see a response from Change indicating that your test donation was successful.

Visit your [Change dashboard](https://api.getchange.io/developers) and click "View test data" to see your donation.