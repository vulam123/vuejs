<template>
  <div>
    <form class="row">
      <div class="form-group col-sm-9">
        <label for="name">Name :</label>
        <input
          v-model="product.name"
          type="text"
          class="form-control"
          id="name"
          placeholder="Enter name"
        />
      </div>
      <div class="form-group col-sm-9">
        <label for="price">Price:</label>
        <input
          v-model="product.price"
          type="email"
          class="form-control"
          id="price"
          placeholder="Enter price"
        />
      </div>
    </form>
    <button type="submit" @click="save()" class="btn btn-primary">Submit</button>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "addproduct",
  data() {
    return {
      product: { name: "", price: "" }
    };
  },
  methods: {
    save() {
      let config = {
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token")
        }
      };
      axios
        .post("http://localhost:8080/products/add", this.product, config)
        .then(res => {
          alert(res.data);
          this.product.name = '';
          this.product.price = '';
        })
        .catch(err => console.log(err));
    }
  }
};
</script>