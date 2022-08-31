<script>
import axios from 'axios'
export default {
  data: function () {
    return {
      message: "Welcome to the Mini-Capstone Store",
      product: {},
      errors: []
    };
  },
  created: function () {
    this.getData()
  },
  methods: {
    getData: function () {
      console.log(`getting data`)
      axios.get(`/products/${this.$route.params.id}.json`).then(response => {
        this.product = response.data
      })
    },
    showDelete: function () {
      console.log("asking if sure")
      document.querySelector("#delete").showModal()
    },
    deleteProduct: function () {
      console.log("deleting product")
      axios.delete(`/products/${this.$route.params.id}`).then(response => {
        console.log(response.data)
      }).catch(error => {
        this.errors = error.response.data.errors;
      })
    }
  },
};
</script>
  
  <template>
  <div class="home">
    <h1>{{  message  }}</h1>
    <h2> {{  product.name  }}</h2>
    <img id="image" v-if="product.images[0]" :src="product.images[0].url"> <br />
    Price: ${{  product.price  }} <br /> <br />
    Description: {{  product.description  }} <br />
    <button v-on:click="addCart">Add to Cart</button> <br /> <br />
    <a v-bind:href="`${this.$route.params.id}/edit`"><button>Edit</button></a>
    <a v-bind:href="`/`"><button>Back</button></a>
    <button v-on:click="showDelete">Delete</button>
    <ul>
      <li v-for="error in errors" v-bind:key="error">{{  error  }}</li>
    </ul>
  </div>

  <dialog id="delete">
    <form method="dialog">
      Are you sure? <br />
      <button v-on:click="deleteProduct">yes</button>
      <button>no</button>
    </form>
  </dialog>
</template>
  
  <style>
  #image {
    height: 200px;
    width: 200px;
  }
  </style>