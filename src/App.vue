<template>
   <!-- <SignUp />     Calling SignUp Component 2.After routing no need to call like this -->
   <!-- router view to call the Home Page , Sign up page After routing -->
   <router-view />        
</template>

<script>

// import signup if we use components but with routing no need to import
// import SignUp from './components/SignUp.vue'
export default {
  name: 'App',

  //No need of components 

  // components: {
  //   SignUp
  // }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body{
  padding:0px;
  margin: 0px;
}

.logo {
    width: 200px;
    margin-top: -60px;
}

.signup{
    margin-top: 5px;
}

.register input, .login input, .add input{
    display: block;
    width: 300px;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 30px;
    height: 30px;
    border: 2px solid cadetblue;

}
.register button, .login button, .add button{
    width: 320px;
    height: 40px;
    background-color: darkseagreen;
    border: 1px solid;
    cursor: pointer;
    color: #fff;
}


</style>
