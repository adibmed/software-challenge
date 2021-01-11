<template>
  <div class="container">
    <div class="row justify-content-center pt-5">
      <div class="col-md-10">
        <div class="card">
          <div class="card-header">
            <button
              type="button"
              class="btn btn-success"
              v-on:click="createProduct"
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
                    <a class="dropdown-item" href="#">name</a>
                  </li>
                  <li>
                    <a class="dropdown-item" href="#">price</a>
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
                    <a class="dropdown-item" href="#">Category 1</a>
                  </li>
                  <li>
                    <a class="dropdown-item" href="#">Category 2</a>
                  </li>
                  <li>
                    <a class="dropdown-item" href="#">Category 3</a>
                  </li>
                  <li>
                    <a class="dropdown-item" href="#">Category 4</a>
                  </li>
                  <li>
                    <a class="dropdown-item" href="#">Category 5</a>
                  </li>
                </ul>
              </div>
            </div>
          </div>

          <div class="card-body">
            <Product
              :v-for="product in products"
              :key="{ product.price }"
              name="{product.name}"
              description="{product.description}"
              price="{product.price}"
              image="{product.image}"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Product from "./components/Product";
export default {
  created: async () => {
      console.log("Component created.");
    // get all the product
    const response = await fetch("http://localhost:8001/api/products/");
    const data = await response.json();
    console.log(data);
    this.products = data;
  },
  data: () => {
    return {
      sort: "name",
      filter: "all",
      products: null,
    };
  },
  components: {
    Product,
  },
  mounted() {
    console.log("Component mounted.");
  },
  methods: {
    createProduct: () => {},
    sortProduct: () => {},
    filterProducts: () => {},
  },
};
</script>
