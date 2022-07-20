<template>

<!-- logo -->
<img class="logo" src="../assets/restro-logo.jpg" />
<h1 class="signup">Login</h1>

<!-- UI part -->

<div class="login">
    <input type="text" placeholder="Enter Email" v-model="email">
    <input type="password" placeholder="Enter Password" v-model="password">
    <button v-on:click="login()">Login</button>
    <p>
        <router-link to="/sign-up">SignUp</router-link>
    </p>
</div>
</template>

<script>
import axios from 'axios'
export default{
    name:'LoginPage',
     data(){
        return{
            email:'',
            password:'',
        }
    },
    methods:{
        async login(){
            let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`);
            console.warn(result)

             if(result.status==200 && result.data.length>0){
                //storing the data in local storage---strigify to convert object data to string
                localStorage.setItem("user-info",JSON.stringify(result.data[0]))
                //Redirect to Home Page
                this.$router.push({name:'Home'})
            }
        }      
    },
    mounted(){
        let user = localStorage.getItem('user-info');
        if(user){
            this.$router.push({name:'Home'})
        }
    }
}
</script>