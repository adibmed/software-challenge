<template>
  <div class="container">
    <div class="row border-top">
      <div class="col-4 bg-secondary p-0">
        <img class="w-100 h-100 img-fluid" v-bind:src="image" alt=""  />
      </div>

      <div class="col-8 py-3">
        <h4>{{ name }}</h4>
        <h6>{{ description }}</h6>
        <h4 class="fond-bold">{{ price }} $</h4>
      </div>
    </div>
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