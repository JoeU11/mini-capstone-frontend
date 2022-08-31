<script>
import axios from 'axios'
export default {
  data: function () {
    return {
      message: "Here is your cart",
      products: [],
      subtotal: 0
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
        this.addSubtotal()
      })
    },
    addSubtotal: function () {
      console.log(this.products)
      this.products.forEach(product => {
        this.subtotal = this.subtotal + product.quantity * product.price
        console.log(this.subtotal)
      })
    }
  },
};
</script>
  
  <template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="product in products">
      {{ product.product }} &nbsp;&nbsp;
      price: {{ product.price }} &nbsp;&nbsp;
      quantity: {{ product.quantity }}
      <br />
    </div>
    <hr />
    <h3>Subtotal: ${{ subtotal }}</h3>
    <p v-if="!products[0]">You have nothing in your cart</p>
  </div>
</template>
  
  <style>
  #image {
    height: 200px;
    width: 200px;
  }
  </style>