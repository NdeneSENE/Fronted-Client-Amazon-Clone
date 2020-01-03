<template>
  <div class="registerPage">
    <div class="container">
      <div class="row">
        <div class="col-sm-4"></div>
        <div class="col-sm-4">
          <div class="text-center">
            <nuxt-link to="/">
              <img src="/img/logo-black.png" alt class />
            </nuxt-link>
            <form class="mt-4">
              <div class="a-box a-spacing-extra-large">
                <div class="a-box-inner">
                  <h1 class="a-spacing-small">Create Account</h1>
                  <div class="row a-spacing-base">
                    <label for="ap_costumer_name" class="a-form-table"
                      >Votre Nom</label
                    >
                    <input
                      type="text"
                      id="ap_costumer_name"
                      class="a-input-text form-control auth-autofocus auth-required-field auth-contact-verification-request-info"
                      v-model="name"
                    />
                  </div>
                  <div class="row a-spacing-base">
                    <label for="ap_costumer_name" class="a-form-table"
                      >Email</label
                    >
                    <input
                      type="email"
                      id="ap_costumer_name"
                      class="a-input-text form-control auth-autofocus auth-required-field auth-contact-verification-request-info"
                      v-model="email"
                    />
                  </div>
                  <div class="row a-spacing-base">
                    <label for="ap_costumer_name" class="a-form-table"
                      >Mot de Passe</label
                    >
                    <input
                      type="password"
                      id="ap_costumer_name"
                      class="a-input-text form-control auth-autofocus auth-required-field auth-contact-verification-request-info"
                      v-model="password"
                    />
                    <div class="a-alert-container">
                      <div class="a-alert-content">
                        Le mot de passe de contenir au moins 6 caractéres.
                      </div>
                    </div>
                    <div class="a-row a-spacing-extra-large mb-4">
                      <span class="a-button-primary">
                        <span class="a-button-inner">
                          <span class="a-button-text" @click="onSignup"
                            >Creer votre compte Amazon</span
                          >
                        </span>
                      </span>
                      <div class="a-row a-spacing-top-medium a-size-small">
                        <b>
                          En créant un compte, vous acceptez
                          <a href="#">les conditions d'utilisations</a> et
                          <a href="#">Notices de confidentialités</a>
                        </b>
                      </div>
                    </div>
                    <hr />
                    <div class="a-row">
                      <b>
                        Vous avez déja un compte?
                        <nuxt-link to="/login" class="a-link-emphasis"
                          >Connecter vous</nuxt-link
                        >
                      </b>
                    </div>
                  </div>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  middleware: "auth",
  auth: "guest",
  layout: "none",
  data() {
    return {
      name: "",
      email: "",
      password: ""
    };
  },
  methods: {
    async onSignup() {
      try {
        let data = {
          name: this.name,
          email: this.email,
          password: this.password
        };
        let response = await this.$axios.$post("/api/auth/signup", data);
        if (response.success) {
          await this.$auth.loginWith("local", {
            data: {
              email: this.email,
              password: this.password
            }
          });
          this.$router.push("/");
        }
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>
