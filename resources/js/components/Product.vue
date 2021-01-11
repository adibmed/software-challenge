<template>
  <div class="container">
    <div class="row">Product {{ name }}</div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: ["name", "description", "price", "image"],
};
</script>

<style>
</style>