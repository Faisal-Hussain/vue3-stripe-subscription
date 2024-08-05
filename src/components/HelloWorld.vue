<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>
      <stripe-checkout ref="checkoutRef" mode="subscription" :pk="publishableKey" :line-items="lineItems"
        :success-url="successURL" :cancel-url="cancelURL" @loading="v => loading = v" />
      <button @click="submit">Pay now!</button>
    </div>
  </div>

</template>

<script>
import { StripeCheckout } from '@vue-stripe/vue-stripe';
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {
    StripeCheckout,
  },
  data() {
    this.publishableKey = 'pk_test_51IQ7cFAFpOTdBwUqzuZbmN15lsrGtucmPCEV66yBot9to7jKxt253szywUuF7GjXgVW0l9FIRvm3U11Jtpc06WxM003zIsKhRU';
    // this.publishableKey = process.env.STRIPE_PUBLISHABLE_KEY;
    return {
      loading: false,
      lineItems: [
        {
          price:  'price_1IyJV8AFpOTdBwUqLTpFnwxS', // The id of the one-time price you created in your Stripe dashboard
          quantity: 1,
        },
      ],
      successURL: 'http://127.0.0.1:8080/',
      cancelURL: 'http://127.0.0.1:8080/',
    };
  },
  methods: {
    submit() {
      console.log(this.$refs,'hdjasdkdsa',this.publishableKey);
      // You will be redirected to Stripe's secure checkout page
      this.$refs.checkoutRef.redirectToCheckout();
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
