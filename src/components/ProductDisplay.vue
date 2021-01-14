<template>
  <div class="product">
    <div class="product__container">
      <div class="product__gallery">
        <img class="product__image" :src="image" alt="" />
      </div>
      <div class="product__info">
        <div class="product__title">
          <h2 class="product__name">{{ title }}</h2>
          <p class="product__description">{{ description }}</p>
          <ul>
            <li v-for="detail in details" :key="detail">
              {{ detail }}
            </li>
          </ul>
        </div>
        <div class="product__details">
          <div class="colors">
            <div
              class="variant__circle"
              v-for="(variant, index) in variants"
              :key="variant.id"
              @click="updateVariant(index)"
              :style="{ backgroundColor: variant.color }"
            ></div>
          </div>
          <button
            class="product__btn btn"
            :class="{ disabledButton: !inStock }"
            :disabled="!inStock"
            @click="addToCart()"
          >
            Add to cart
          </button>
          <p>Shipping: {{ shipping }}</p>
          <span v-if="inventory > 10">In Stock</span>
          <p v-else-if="inventory <= 10">Almost Sold Out</p>
          <span v-else>Out Of Stock</span>
        </div>
      </div>
    </div>
    <review-form @review-submitted="addReview" />
    <review-list v-if="reviews.length" :reviews="reviews" />
  </div>
</template>
<script>
import ReviewForm from "./ReviewForm";
import ReviewList from "./ReviewList";
export default {
  name: "ProductDisplay",
  components: {
    ReviewForm,
    ReviewList,
  },
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      selectedVariant: 0,
      brand: "Levi´s",
      product: "Socks",
      description:
        "A sock is a piece of clothing worn on the feet and often covering the ankle or some part of the calf. Some type of shoe or boot is typically worn over socks. In ancient times, socks were made from leather or matted animal hair. In the late 16th century, machine-knit socks were first produced.",
      inventory: 9,
      details: ["50% cotton", "30% wool", "20% polyester"],
      variants: [
        {
          id: 2324,
          color: "green",
          image: require("../assets/images/socks_green.jpg"),
          quantity: 50,
        },
        {
          id: 6234,
          color: "blue",
          image: require("../assets/images/socks_blue.jpg"),
          quantity: 0,
        },
      ],
      reviews: [],
    };
  },
  methods: {
    addToCart() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].id);
    },
    updateVariant(index) {
      this.selectedVariant = index;
    },
    addReview(review) {
      this.reviews.push(review);
    },
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].image;
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity;
    },
    shipping() {
      if (this.premium) {
        return "Free";
      }
      return "$10.00";
    },
  },
};
</script>
<style>
.product__info {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}
.product__name {
  font-size: 33px;
  font-weight: 700;
  margin-top: 15px;
}
.product__info ul {
  list-style: none;
  color: #585858;
  font-size: 12px;
  display: flex;
  margin-top: 8px;
}
.product__info ul li {
  margin-bottom: 5px;
  margin-right: 10px;
}
.product__description {
  font-size: 12px;
  line-height: 20px;
}
.variant__circle {
  width: 35px;
  height: 35px;
  margin-top: 8px;
  border: 2px solid #d8d8d8;
  border-radius: 50%;
  cursor: pointer;
}
.variant__circle:first-child {
  margin-right: 5px;
}
.colors {
  display: flex;
}
</style>
