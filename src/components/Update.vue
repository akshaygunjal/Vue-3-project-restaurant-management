<template>
    <Header/>
    <h1>Hello {{name}}, Welcome to Update Restaurant Page</h1>
        <form class="add">
        <input type="text" placeholder="Enter Restaurant Name" v-model="restaurants.name" name="name" />
        <input type="text" placeholder="Enter Restaurant Address" v-model="restaurants.address" name="address" />
        <input type="text" placeholder="Enter Restaurant Contact" v-model="restaurants.contact" name="contact" />
        <button type="button" v-on:click="updateRestaurants()">Update  Restaurant</button>
    </form>
</template>
<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
    name:'UpdatePage',
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
        async updateRestaurants(){
            console.warn("function called",this.restaurants);
            let result = await axios.put('http://localhost:3000/restaurants/'+this.$route.params.id,
            {
                name:this.restaurants.name,
                address:this.restaurants.address,
                contact:this.restaurants.contact 
            });
            console.warn(result,"result")
            if(result.status==200){
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
        let result = await axios.get('http://localhost:3000/restaurants/'+this.$route.params.id);
        console.warn(result.data)
        this.restaurants=result.data
        // console.warn(this.$route.params.id)
    }
}
</script>