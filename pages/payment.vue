<template>
  <main class="listingPage">
    <div class="container">
      <div class="a-section">
        <h2>Effectuez le paiement.</h2>
      </div>
      <div class="a-section a-spacing-none a-spacing-top-small">
        <b>Prix total: ${{ getCartTotalPriceWithShipping }}</b>
      </div>
      <form action="#" method="POST">
        <div class="a-spacing-medium a-spacing-top-medium">
          <div ref="card"></div>
        </div>
        <div class="a-spacing-top-medium"></div>
        <div class="a-spacing-top-medium">
          <span>
            <b>
              Soyez sure que votre adresse est correcte.
            </b>
          </span>
        </div>
        <div class="a-row text-right a-spacing-top-large">
          <span class="a-button-register">
            <span class="a-button-inner">
              <span class="a-button-text" @click="onPurchase">Payez</span>
            </span>
          </span>
        </div>
        <hr />
      </form>
    </div>
  </main>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  data() {
    return {
      error: "",
      stripe: null,
      card: null
    };
  },
  mounted() {
    this.stripe = Stripe("pk_test_A0jhPuZSLO1R8yJfOgF4nVlD");
    let elements = this.stripe.elements();
    this.card = elements.create("card");
    this.card.mount(this.$refs.card);
  },
  computed: {
    ...mapGetters([
      "getCart",
      "getCartTotalPriceWithShipping",
      "getEstimatedDeliver"
    ])
  },
  methods: {
    async onPurchase() {
      try {
        let token = await this.stripe.createToken(this.card);
        let response = await this.$axios.$post("/api/payment", {
          token: token,
          totalPrice: this.getCartTotalPriceWithShipping,
          cart: this.getCart,
          estimatedDelivery: this.getEstimatedDeliver
        });
        console.log(response, token);
        if (response.success) {
          this.$store.commit("clearCart");
          this.$router.push("/orders");
        }
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>

<style>
.StripeElement {
  box-sizing: border-box;

  height: 40px;

  padding: 10px 12px;

  border: 1px solid transparent;
  border-radius: 4px;
  background-color: white;

  box-shadow: 0 1px 3px 0 #e6ebf1;
  -webkit-transition: box-shadow 150ms ease;
  transition: box-shadow 150ms ease;
}

.StripeElement--focus {
  box-shadow: 0 1px 3px 0 #cfd7df;
}

.StripeElement--invalid {
  border-color: #fa755a;
}

.StripeElement--webkit-autofill {
  background-color: #fefde5 !important;
}
</style>
