<script>
import axios from 'axios'
export default {
  data: function () {
    return {
      message: "Here is your cart",
      products: []
    };
  },
  created: function () {
    this.getData()
  },
  methods: {
    getData: function () {
      console.log(`getting data`)
      axios.get("/carted_products.json").then(response => {
        this.products = response.data
      })
    }
  },
};
</script>
  
  <template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="product in products">
      Product: {{ product.product }} &nbsp;&nbsp;
      price: {{ product.price }} &nbsp;&nbsp;
      quantity: {{ product.quantity }}
      <br />
    </div>
    <p v-if="!products[0]">You have nothing in your cart</p>
  </div>
</template>
  
  <style>
  #image {
    height: 200px;
    width: 200px;
  }
  </style>