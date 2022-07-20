<template>
<Header />
<h1>Hello {{User}}, Welcome On Home Page</h1>
<table class ="table" border="1px">
<tr>
    <td>Id</td>
    <td>Name</td>
    <td>Address</td>
    <td>Contact</td>
    <td>Actions</td>
</tr>
<tr v-for="item in restaurants" :key="item">
    <td>{{item.id}}</td>
    <td>{{item.name}}</td>
    <td>{{item.address}}</td>
    <td>{{item.contact}}</td>
    <td><router-link :to="'/update/'+item.id">Update</router-link>
    <button v-on:click="deleteRestaurants(item.id)">Delete</button></td>
</tr>
</table>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name: 'HomePage',
    data(){
        return{
            name:'',
            restaurants:[]
        } 
    },
    components: {
        Header
    },
    methods:{
        async deleteRestaurants(id){
            let result = await axios.delete('http://localhost:3000/restaurants/'+id);
            if(result.status==200){
                this.loadData()
            }    
        },
        async loadData(){
             let user = localStorage.getItem('user-info');
            this.name=JSON.parse(user).name;
            if (!user) {
                this.$router.push({
                    name: 'SignUp'
                })
            }
            let result = await axios.get('http://localhost:3000/restaurants');
            console.warn(result)
            this.restaurants=result.data
        }
    },
    
    mounted() {
       this.loadData()
    }
}
</script>
<style>

.table{
    margin-left:auto;
    margin-right:auto;
}
td{
    width:180px;
    height:40px;
    
}
</style>