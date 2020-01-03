<template>
  <main class="listingPage">
    <div class="container">
      <div class="row">
        <div class="col-xl-2 col-lg-3 md-4 col-sm-4"></div>
        <div class="col-xl-10 col-lg-9 md-8 col-sm-8">
          <FeaturedProduct />
          <div class="mainResults">
            <ul class="s-result-list">
              <li
                class="s-result-item celwidget"
                v-for="(product, index) in products"
                :key="product._id"
              >
                <div class="s-item-container">
                  <div class="a-spacing-micro">
                    <div class="bestSeller">
                      <a href="#">Best Seller</a>
                    </div>
                  </div>
                  <div class="row">
                    <div class="col-sm-3 text-center">
                      <a href="#">
                        <img
                          :src="product.photo"
                          style="width: 150px"
                          class="img-fluid"
                        />
                      </a>
                    </div>
                    <div class="col-sm-9">
                      <div class="a-row a-spacing-small">
                        <nuxt-link
                          class="a-link-normal"
                          :to="`/products/${product._id}`"
                        >
                          <h2 class="a-size-medium">
                            {{ product.title }}
                            <span class="a-letter-space"></span>
                            <span class="a-letter-space"></span>
                            <span class="a-size-small a-color-secondary"
                              >21 Décembre 2019</span
                            >
                          </h2>
                        </nuxt-link>
                      </div>
                      <div class="a-row a-spacing-small">
                        <span class="a-size-small a-color-secondary">By</span>
                        <span class="a-size-small a-color-secondary">
                          <a href="#" class="a-link-normal a-text-normal">{{
                            product.owner.name
                          }}</a>
                        </span>
                      </div>
                      <div class="a-row">
                        <span class="a-size-small">Ships To USA</span>
                      </div>
                      <div class="row">
                        <div class="col-sm-7">
                          <div class="a-row a-spacing-none">
                            <a href="#" class="a-link-normal a-text-normal"
                              >Hardcover</a
                            >
                          </div>
                          <div class="a-row a-spacing-none">
                            <a href="#" class="a-link-normal a-text-normal">
                              <span class="a-offscreen"
                                >$ {{ product.price }}</span
                              >
                              <span class="a-color-base sx-zero-spacing">
                                <span class="sx-price sx-price-large">
                                  <sup class="sx-price-currency">$</sup>
                                  <sup class="sx-price-whole">{{
                                    product.price
                                  }}</sup>
                                  <sup class="sx-price-fractional">00</sup>
                                </span>
                              </span>
                            </a>
                            <span class="a-letter-space"></span>
                            <span
                              class="a-size-base-plus a-color-secondary a-text-strike"
                              >$90</span
                            >
                          </div>
                          <div class="a-row a-spacing-none">
                            <span class="a-size-small a-color-secondary"
                              >Free with audible Trial</span
                            >
                          </div>
                          <hr />
                          <span class="a-size-small a-color-secondary">
                            Others Formats:
                            <span class="a-letter-space"></span>
                            <a
                              href="#"
                              class="a-size-small a-link-normal a-text-normal"
                              >Audio CD</a
                            >
                          </span>
                        </div>
                        <div class="col-sm-5">
                          <div class="a-row a-spacing-mini">
                            <client-only>
                              <star-rating
                                :rating="product.averageRating"
                                :show-rating="false"
                                :glow="1"
                                :border-width="1"
                                :rounded-corners="true"
                                :read-only="true"
                                :star-size="18"
                                :star-points="[
                                  23,
                                  2,
                                  14,
                                  17,
                                  0,
                                  19,
                                  10,
                                  34,
                                  7,
                                  50,
                                  23,
                                  43,
                                  38,
                                  50,
                                  36,
                                  34,
                                  46,
                                  19,
                                  31,
                                  17
                                ]"
                              ></star-rating>
                            </client-only>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import StarRating from "vue-star-rating";

import FeaturedProduct from "~/components/FeaturedProduct.vue";
export default {
  components: {
    FeaturedProduct,
    StarRating
  },
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get("/api/products");

      return {
        products: response.products
      };
    } catch (error) {
      console.log(error);
    }
  }
};
</script>
