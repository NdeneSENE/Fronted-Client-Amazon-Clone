<template>
  <!--MAIN-->
  <main>
    <!--REGISTER ADDRESS-->
    <div class="registerAddress mt-3">
      <div class="container-fluid c-section">
        <div class="row">
          <div class="col-sm-3"></div>
          <div class="col-sm-6">
            <div class="a-section a-spacing-medium">
              <div class="a-subheader a-breadcrumb a-spacing-small">
                <ul>
                  <li>
                    <a href="#">
                      <span>Your Account</span>
                    </a>
                  </li>
                  <li class="a-breadcrumb-divider">›</li>
                  <li>
                    <a href="#">
                      <span>Your Adresses</span>
                    </a>
                  </li>
                  <li class="a-breadcrumb-divider">›</li>
                  <li class="active">
                    <a href="#">
                      <span>New Address</span>
                    </a>
                  </li>
                </ul>
              </div>
            </div>
            <div class="a-section">
              <h2>Modifier l'address</h2>
              <div class="a-section a-spacing-none a-spacing-top-small">
                <b>
                  Or pick up your packages at your convenience from our
                  self-service locations. To add an Amazon Pickup Point or
                  Locker, click
                  <a href="#">here</a>.
                </b>
              </div>
              <!-- Error Message -->
              <div class="a-section a-spacing-none a-spacing-top-small">
                <b></b>
              </div>
              <form>
                <div class="a-spacing-medium a-spacing-top-medium">
                  <!-- Country / Region -->
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;">Country/Region</label>
                    <select class="a-select-option" v-model="country">
                      <option
                        v-for="country in countries"
                        :key="country.alpha2Code"
                        :value="country.name"
                        >{{ country.name }}</option
                      >
                      <option></option>
                    </select>
                  </div>
                  <!-- Full name -->
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;">Full Name</label>
                    <input
                      type="text"
                      class="a-input-text"
                      style="width: 100%;"
                      v-model="fullName"
                      :placeholder="adresse.fullName"
                    />
                  </div>
                  <!-- Street Address -->
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;">Street Address</label>
                    <input
                      type="text"
                      class="a-input-text"
                      style="width: 100%;"
                      v-model="streetAdress1"
                      :placeholder="adresse.streetAdress"
                    />
                    <!-- Street Address 2 -->
                    <input
                      type="text"
                      class="a-input-text a-spacing-top-small"
                      style="width: 100%;"
                      v-model="streetAdress2"
                      :placeholder="adresse.streetAdress2"
                    />
                  </div>
                  <!-- City -->
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;">City</label>
                    <input
                      type="text"
                      class="a-input-text"
                      style="width: 100%;"
                      v-model="city"
                      :placeholder="adresse.city"
                    />
                  </div>
                  <!-- State -->
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;"
                      >State / Province / Region</label
                    >
                    <input
                      type="text"
                      class="a-input-text"
                      style="width: 100%;"
                      v-model="state"
                      :placeholder="adresse.state"
                    />
                  </div>
                  <!-- Zip Code -->
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;">Zip Code</label>
                    <input
                      type="text"
                      class="a-input-text"
                      style="width: 100%;"
                      v-model="zipCode"
                      :placeholder="adresse.zipCode"
                    />
                  </div>
                  <!-- Phone Number -->
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;">Phone Number</label>
                    <input
                      type="text"
                      class="a-input-text"
                      style="width: 100%;"
                      v-model="phoneNumber"
                      :placeholder="adresse.phoneNumber"
                    />
                    <div class="a-section a-spacing-none a-spacing-top-micro">
                      <span class="a-size-mini"
                        >May be used to assist delivery</span
                      >
                    </div>
                  </div>
                  <div class="a-spacing-base a-spacing-top-medium">
                    <h3>Add delivery instructions</h3>
                  </div>
                  <!-- Delivery Instruction -->
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;">
                      Do we need additional instructions to find this address?
                    </label>
                    <textarea
                      style="height:6em; width: 100%;"
                      v-model="deliveryInstructions"
                      :placeholder="adresse.deliveryInstructions"
                    ></textarea>
                  </div>
                  <!-- Security code -->
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;">
                      Do we need a security code or a call box number to access
                      this building?
                    </label>
                    <input
                      type="text"
                      class="a-input-text"
                      style="width: 100%;"
                      v-model="securityCode"
                      :placeholder="adresse.securityCode"
                    />
                  </div>
                  <div class="a-spacing-top-medium">
                    <label style="margin-bottom: 0px;">Weekend delivery</label>
                    <a href="#">
                      <i class="fas fa-angle-down"></i> Which days can you
                      receive packages?
                    </a>
                  </div>
                  <div class="a-spacing-top-medium"></div>
                  <hr />
                  <div class="a-spacing-top-medium">
                    <span>
                      <b>Make sure your address is correct</b>
                    </span>
                  </div>
                  <div>
                    <span>
                      If the address contains typos or other errors, your
                      package may be undeliverable.
                    </span>
                  </div>
                  <div class="a-spacing-top-small">
                    <span>
                      <a href="#">Tips for entering addresses</a>
                    </span>
                    <span>|</span>
                    <span>
                      <a href="#">APO/FPO address tips</a>
                    </span>
                  </div>
                  <div class="a-spacing-top-large">
                    <span class="a-button-register">
                      <span class="a-button-inner">
                        <span class="a-button-text" @click="onUpdateAdress"
                          >Modifier address</span
                        >
                      </span>
                    </span>
                  </div>
                </div>
              </form>
            </div>
          </div>
          <div class="col-sm-3"></div>
        </div>
      </div>
    </div>
    <!--/REGISTER ADDRESS-->
  </main>
  <!--/MAIN-->
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    try {
      let country = $axios.$get("/api/country");
      let singleAdress = $axios.$get(`/api/adresses/${params.id}`);
      let [countryResponse, adressResponse] = await Promise.all([
        country,
        singleAdress
      ]);

      return {
        countries: countryResponse,
        adresse: adressResponse.adresse
      };
    } catch (error) {
      console.log(error);
    }
  },
  data() {
    return {
      country: "Senegal",
      fullName: "",
      streetAdress1: "",
      streetAdress2: "",
      city: "",
      state: "",
      zipCode: "",
      phoneNumber: "",
      deliveryInstructions: "",
      securityCode: ""
    };
  },
  methods: {
    async onUpdateAdress() {
      try {
        let data = {
          country: this.country,
          fullName: this.fullName,
          streetAdress: this.streetAdress1 + " " + this.streetAdress2,
          city: this.city,
          state: this.state,
          zipCode: this.zipCode,
          phoneNumber: this.phoneNumber,
          deliveryInstructions: this.deliveryInstructions,
          securityCode: this.securityCode
        };
        let response = await this.$axios.$put(
          `/api/adresses/${this.$route.params.id}`,
          data
        );

        if (response.success) {
          this.$router.push("/adress");
        }
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>
