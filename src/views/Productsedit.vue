<script>
import axios from "axios";

export default {
  data: function () {
    return {
      product: {},
      errors: [],
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
    submit: function () {
      axios
        .patch(`/products/${this.product.id}.json`, this.product)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/products/${this.product.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
  
  <template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1> Editing Product </h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{  error  }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="product.name" />
      </div>
      <div>
        <label>Price:</label>
        <input type="number" v-model="product.price" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="product.description" />
      </div>
      <!-- <div> -->
      <!-- <label>Image URL</label> -->
      <!-- <input type="text" v-model="product." /> -->
      <!-- </div> -->
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>