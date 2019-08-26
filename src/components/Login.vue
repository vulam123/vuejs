<template>
  <div>
    <b-form-group id="input-group-1" label="Email address:" label-for="input-1">
      <b-form-input
        id="input-1"
        v-model="form.email"
        type="email"
        required
        placeholder="Enter email"
      ></b-form-input>
    </b-form-group>

    <b-form-group id="input-group-2" label="Password:" label-for="input-2">
      <b-form-input
        id="input-2"
        v-model="form.password"
        type="password"
        required
        placeholder="Enter password"
      ></b-form-input>
    </b-form-group>
    <b-button type="submit" @click="login" variant="primary">Submit</b-button>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      form: { email: "", password: "" }
    };
  },
  methods: {
    login() {
      axios
        .post("http://localhost:8080/login", {
          username: this.form.email,
          password: this.form.password
        })
        .then(res => {
          console.log(res);
          localStorage.setItem("token", res.data.jwt);
          localStorage.setItem("role", res.data.role);

        })
        .catch(err => console.log(err));
    }
  },
  mounted(){
      if(localStorage.getItem("token")!==null&&localStorage.getItem("token")!==undefined){
          if(localStorage.getItem("role")!==null&&localStorage.getItem("token")!==undefined&&localStorage.getItem("role")==="ROLE_USER")
          this.$router.push({ path: 'user/viewproduct' })
      }
  }
};
</script>