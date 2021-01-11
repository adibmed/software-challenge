<template>
  <div class="container">
    <div class="row">Product {{ name }}</div>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    description: String,
    price: Number,
    image: String,
  },
};
</script>

<style>
</style>