<template>
  <div id="nav">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <router-link v-bind:class="{active:currentlink==='viewproduct'}" @click.native="change('viewproduct')" class="nav-item nav-link" to="/user/viewproduct">View product</router-link>
          <router-link v-bind:class="{active:currentlink==='addproduct'}"  @click.native="change('addproduct')" class="nav-item nav-link" to="/user/addproduct">Add product</router-link>
        </div>
      </div>
    </nav>
    <router-view v:on-highlight="highlight"/>
  </div>
</template>
<script>
export default {
    name: "Usermenu",
    data(){
        return {
            currentlink : ''
        }
    },
    methods:{
        change(url){
            this.currentlink = url
            console.log(url)
        }
    },
    mounted(){
            this.currentlink = this.$route.name
        }
    }
    
</script>