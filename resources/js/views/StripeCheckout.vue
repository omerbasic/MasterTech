<template>
  <!-- stripe-checkout -->
  <div>
    <stripe-checkout
      ref="checkoutRef"
      mode="payment"
      :pk="publishableKey"
      :line-items="lineItems"
      :success-url="successURL"
      :cancel-url="cancelURL"
      @loading="v => loading = v"
    />
    <h1>Proceed to Stripe Checkout</h1>
    <button @click="submit">Pay now!</button>
  </div>
</template>

<script>
import { StripeCheckout } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeCheckout,
  },
  data () {
    this.publishableKey = 'pk_test_51HMTldKEUIKsCRFh6xC4GVU96lW0bbRsLDsYszzZEJUwLsSgNK3pOYv1RLWfBHHkVHONcNQdtJkB6mhXvQBkmdxw00nd03I4rP';
    let orderArray = JSON.parse(localStorage.getItem('bigStore.cart'));
    console.log("test");
    console.log(orderArray);
    let formattedProducts = orderArray.map((product) => {
            return {
                price: product.product_api, // The id of the one-time price you created in your Stripe dashboard
                quantity: product.quantity,
            }
            
        })
    return {
      loading: false,
      lineItems: formattedProducts,
      successURL: 'http://134.122.98.190/confirmation',
      cancelURL: 'https://google.se',
    };
  },
    methods: {
        // You will be redirected to Stripe's secure checkout page
     submit () {
       let orderArray = JSON.parse(localStorage.getItem('bigStore.cart'));
        console.log("test");
        console.log(orderArray);
         this.$refs.checkoutRef.redirectToCheckout();
    },  
    },
};


</script>