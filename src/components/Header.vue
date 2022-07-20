<template>
  <div class="nav">
    <router-link to="/">Home</router-link>
    <router-link to="/add">Add Restaurant</router-link>
    <a v-on:click="logout()" href="#">Logout</a>
  </div>
  
</template>
<script>
export default {
    name:'HeaderPage',
    methods:{
        logout(){
            localStorage.clear()
            this.$router.push({name:'Login'})
        }
    }
}
</script>
<style>
.nav{
    background-color: #333;
    overflow: hidden;
}
.nav a{
    float: left;
    color: aliceblue;
    text-align: center;
    padding: 10px 14px;
    font-size: 16px;
    text-decoration: none;
    margin-right: 4px;
}
.nav a:hover{
    background-color:#ddd ;
    color:#222;
}

</style>