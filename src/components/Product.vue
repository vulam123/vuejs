<template>
  <div>
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">First</th>
          <th scope="col">Last</th>
          <th scope="col">Update</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item,index) in list" v-bind:key="item.id">
          <th scope="row">{{index}}</th>
          <td>
            <input type="text" v-model="item.name" />
          </td>
          <td>
            <input type="text" v-model="item.price" />
          </td>
          <td>
            <button @click="update(item)" type="button" class="btn btn-primary">Update</button>
          </td>
          <td>
            <button @click="Delete(item.id)" type="button" class="btn btn-danger">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Product",
  data() {
    return {
      list: []
    };
  },
  methods: {
    Delete(id) {
        let config = {
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token")
        }
      };
      axios
        .post("http://localhost:8080/products/delete/"+id, config)
        .then(res => {
          alert(res.data);
          this.getData();
        })
        .catch(err => console.log(err));

    },
    update(item) {
      let config = {
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token")
        }
      };
      axios
        .post("http://localhost:8080/products/update", item, config)
        .then(res => {
          alert(res.data);
        })
        .catch(err => console.log(err));
    }
    ,
    getData(){
        let config = {
      headers: {
        Authorization: "Bearer " + localStorage.getItem("token")
      }
    };
    axios
      .get("http://localhost:8080/products/getall", config)
      .then(res => {
        this.list = res.data;
      })
      .catch(err => console.log(err));
    }
  },
  mounted() {
    this.getData();
  }
};
</script>
<style scoped>
input[type="text"] {
  border: none;
}
</style>