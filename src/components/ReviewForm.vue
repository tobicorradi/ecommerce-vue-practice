<template>
  <form @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input required v-model="name" id="name" name="name" type="text" />
    <label for="Review">Review:</label>
    <textarea required v-model="review" id="review" name="review" type="text" />
    <label for="rating">Rating:</label>
    <select required v-model.number="rating" name="rating" id="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>
    <input type="submit" value="submit" />
  </form>
</template>
<script>
export default {
  name: "ReviewForm",
  data() {
    return {
      name: "",
      review: "",
      rating: null,
    };
  },
  methods: {
    onSubmit() {
      let productReview = {
        name: this.name,
        review: this.review,
        rating: this.rating,
      };
      this.$emit("review-submitted", productReview);
      this.name = "";
      this.review = "";
      this.rating = null;
    },
  },
};
</script>
