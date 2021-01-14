<template>
  <div class="review">
    <h3>Reviews:</h3>
    <ul>
      <li v-for="review in reviews" :key="review.name">
        <p>{{ review.name }} gave this {{ review.rating }} stars</p>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "ReviewList",
  props: {
    reviews: {
      type: Array,
      required: true,
    },
  },
};
</script>
