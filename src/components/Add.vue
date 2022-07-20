<template>
    <Header/>
    <h1>Hello User, Welcome to Add Restaurant Page</h1>
    <form class="add">
        <input type="text" placeholder="Enter Restaurant Name" v-model="restaurants.name" name="name" />
        <input type="text" placeholder="Enter Restaurant Address" v-model="restaurants.address" name="address" />
        <input type="text" placeholder="Enter Restaurant Contact" v-model="restaurants.contact" name="contact" />
        <button type="button" v-on:click="addRestaurants()">Add New Restaurant</button>
    </form>
</template>
<script>

import Header from './Header.vue'
import axios from 'axios'
export default {
    name:'AddPage',
    data(){
        return{
            restaurants:{
                name:'',
                address:'',
                contact:'',
            }  
        }
    },
    methods:{
        async addRestaurants(){
            console.warn(this.restaurants)
            console.warn("Added Restaurants",this.restaurants.name,this.restaurants.address,this.restaurants.contact)

            //install axios to use api's
            //Use post coz we need to store data
            //await and async coz data may not come in sync manner

            let result = await axios.post('http://localhost:3000/restaurants',
            {
                name:this.restaurants.name,
                address:this.restaurants.address,
                contact:this.restaurants.contact 
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
    components:{
        Header
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({
                name: 'SignUp'
            })
        }
    }
}
</script>