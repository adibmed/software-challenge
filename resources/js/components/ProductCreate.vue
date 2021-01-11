<template>
  <div class="p-4">
    <div class="btn-group">
      <button
        type="button"
        class="btn btn-primary dropdown-toggle"
        data-bs-toggle="dropdown"
        aria-expanded="false"
      >
        Category
      </button>
      <ul class="dropdown-menu">
        <li v-for="category in categories" :key="category.id">
          <a @click="setCategory(category.id)" class="dropdown-item" href="#">{{
            category.name
          }}</a>
        </li>
      </ul>
    </div>

    <div class="mb-3 pt-3">
      <label for="product-name" class="form-label">Name</label>
      <input
        type="text"
        class="form-control"
        id="product-name"
        v-model="name"
      />
    </div>
    <div class="mb-3">
      <label for="product-description" class="form-label">Description</label>
      <textarea
        v-model="description"
        class="form-control"
        id="product-description"
        rows="3"
      ></textarea>
    </div>

    <div class="mb-3">
      <label for="product-price" class="form-label">Price</label>
      <input
        v-model="price"
        type="text"
        class="form-control"
        id="product-price"
      />
    </div>

    <div class="mb-3">
      <label for="product-image" class="form-label">Image</label>
      <input
        v-model="imageUrl"
        type="text"
        class="form-control"
        id="product-image"
      />
    </div>

    <button
      @click="createProduct"
      type="button"
      class="btn btn-primary float-right px-5"
    >
      Add Product
    </button>
  </div>
</template>

<script>
export default {
  name: "ProductCreate",
  props: ["categories"],
  data: () => {
    return {
      name: "",
      description: "",
      price: null,
      imageUrl: null,
      category_id: null,
    };
  },
  methods: {
    async createProduct() {
      const product = {
        name: this.name,
        description: this.description,
        price: this.price,
        image: this.imageUrl,
        category_id: this.category_id,
      };

      const rawResponse = await fetch("http://localhost:8001/api/products", {
        method: "POST",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
        body: JSON.stringify(product),
      });
      const content = await rawResponse.json();
      this.$emit("refreash-products");
    },
    setCategory(id) {
      this.category_id = id;
    },
  },
};
</script>

<style>
</style>