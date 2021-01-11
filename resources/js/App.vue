<template>
  <div class="container">
    <div v-if="showPopup" class="row justify-content-center pt-5">
      <div class="col-md-10">
        <div class="card">
          <div class="card-header">Add New Product</div>
          <div class="card-body">
            <ProductCreate
              :categories="categories"
              v-on:refreash-products="refreashProducts"
            />
          </div>
        </div>
      </div>
    </div>

    <div class="row justify-content-center pt-5">
      <div class="col-md-10">
        <div class="card">
          <div class="card-header">
            <button
              type="button"
              class="btn btn-success"
              v-on:click="showPopup = !showPopup"
            >
              Create
            </button>

            <div class="float-right">
              <div class="btn-group">
                <button
                  type="button"
                  class="btn btn-primary dropdown-toggle"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  Sort by
                </button>
                <ul class="dropdown-menu">
                  <li>
                    <a
                      class="dropdown-item"
                      href="#"
                      @click="sortProduct('name')"
                      >name</a
                    >
                  </li>
                  <li>
                    <a
                      class="dropdown-item"
                      href="#"
                      @click="sortProduct('price')"
                      >price</a
                    >
                  </li>
                </ul>
              </div>

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
                  <li>
                    <a
                      class="dropdown-item"
                      href="#"
                      @click="filterProducts(-1)"
                      >All</a
                    >
                  </li>
                  <li v-for="category in categories" :key="category.id">
                    <a
                      class="dropdown-item"
                      href="#"
                      @click="filterProducts(category.id)"
                      >{{ category.name }}</a
                    >
                  </li>
                </ul>
              </div>
            </div>
          </div>

          <div
            class="card-body m-0 p-0"
            v-for="product in products"
            :key="product.id"
          >
            <Product
              :key="product.price"
              :name="product.name"
              :description="product.description"
              :price="product.price"
              :image="product.image"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Product from "./components/Product";
import ProductCreate from "./components/ProductCreate";
export default {
  data: () => {
    return {
      sort: "name",
      filter: "all",
      products: null,
      categories: null,
      showPopup: false,
      oldProducts: null,
    };
  },
  components: {
    Product,
    ProductCreate,
  },
  mounted() {
    console.log("Component mounted.");
  },
  methods: {
    sortProduct(type) {
      console.log("sort-->" + type);

      this.product = this.arrays.sort(() => {
        if (this.sort === "name") {
          if (a.name < b.name) return -1;
          if (a.name > b.name) return 1;
        } else if (this.sort === "price") {
          if (a.price < b.price) return -1;
          if (a.price > b.price) return 1;
        }

        return 0;
      });
    },
    filterProducts(categoryId) {
      this.products = this.oldProducts;
      console.log(this.oldProducts);
      if (categoryId != -1) {
        const newProducts = this.products.filter(
          (product) => product.category_id == categoryId
        );
        this.products = newProducts;
      } else {
        this.products = this.oldProducts;
      }
    },
    showCreateProduct: () => {
      showPopup = !showPopup;
    },
    refreashProducts() {
      fetch("http://localhost:8001/api/products/")
        .then((response) => response.json())
        .then((data) => {
          this.products = data;
          this.oldProducts = data;
        });

      fetch("http://localhost:8001/api/categories/")
        .then((response) => response.json())
        .then((data) => {
          this.categories = data;
        });

      this.showPopup = false;
    },
  },
  mounted: function () {
    this.refreashProducts();
  },
  computed: {
    sortedProducts: function () {
      function compare(a, b) {
        if (this.sort === "name") {
          if (a.name < b.name) return -1;
          if (a.name > b.name) return 1;
        } else if (this.sort === "price") {
          if (a.price < b.price) return -1;
          if (a.price > b.price) return 1;
        }

        return 0;
      }

      return this.arrays.sort(compare);
    },
  },
};
</script>


<style>
</style>