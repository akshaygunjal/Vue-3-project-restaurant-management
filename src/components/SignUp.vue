<template>

<!-- logo -->
<img class="logo" src="../assets/restro-logo.jpg" />
<h1 class="signup">Sign Up</h1>

<!-- UI part -->

<div class="register">
    <input type="text" placeholder="Enter Username" v-model="name">
    <input type="text" placeholder="Enter Email" v-model="email">
    <input type="password" placeholder="Enter Password" v-model="password">
    <button v-on:click="signUp()">Sign Up</button>
    <p>
        <router-link to="/login">Login</router-link>
    </p>
</div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'SignUp',
    // user input data stored in name,email,password
    data(){
        return{
            name:'',
            email:'',
            password:'',
        }
    },
    methods:{
        //to connect api 
        async signUp(){
            console.warn("SignUp Working",this.name,this.email,this.password)

            //install axios to use api's
            //Use post coz we need to store data
            //await and async coz data may not come in sync manner

            let result = await axios.post('http://localhost:3000/users',
            {
                name:this.name,
                email:this.email,
                password:this.password 
            });
            console.warn(result,"result")
            if(result.status==201){
                //storing the data in local storage---strigify to convert object data to string
                localStorage.setItem("user-info",JSON.stringify(result.data))
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

