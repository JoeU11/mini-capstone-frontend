<script>
import axios from 'axios'
export default {
  data: function () {
    return {
      message: "Welcome to the Mini-Capstone Store",
      products: []
    };
  },
  created: function () {
    this.getData()
  },
  methods: {
    getData: function () {
      console.log(`getting data`)
      axios.get("/products.json").then(response => {
        this.products = response.data
      })
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{  message  }}</h1>
    <h2>Products:</h2>
    <div v-for="product in products">
      <img id="image" v-if="product.images[0]" :src="product.images[0].url"> <br />
      Product: {{  product.name  }} <br />
      {{  product.price  }} <br />
      <a v-bind:href="`products/${product.id}`"><button>details</button></a>
      <hr />
    </div>
  </div>
</template>

<style>
#image {
  height: 200px;
  width: 200px;
}
</style>