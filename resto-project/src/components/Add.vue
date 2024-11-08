<template>
    <Header />    
    <div class="headContainer">
        <div class="container-2">
            <h1> Add Restaurant</h1>
            <div class="add">
                <input type="text" name="addname" placeholder="Enter Restaurent Name" v-model="addname"/>
                <input type="text" name="address" placeholder="Enter Restaurent Address" v-model="address"/>
                <input type="text" name="contact" placeholder="Enter Restaurent Contact" v-model="contact"/>
                <button type="button" v-on:click="addRestaurent">Add Restaurant</button>
            </div>
            
        </div>
    
        <div class="container-1">
    
            <table border="1">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Name</th>
                        <th>Address</th>
                        <th>Contact</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in resturants" :key="item.id">
                        <td>{{ item.id }}</td>
                        <td>{{ item.name }}</td>
                        <td>{{ item.address }}</td>
                        <td>{{ item.contact }}</td>
                        <td>
                            <router-link :to="'/update/'+item.id ">Update</router-link>
                            <button v-on:click="deleteResturant(item.id)" class="btn">Delete</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
       <div class="popupx">

       </div>


    </div>
    
    </template>
  
  
<script>
import axios from 'axios'
import Header from './Header.vue'
export default{
    name:'Add',
    components:{
    Header
    },
    data()
    {
        return{
            addname:'',
            address:'',
            contact:'',
            name:'',
            resturants:[],
        }
    },
    methods:      
    {
        async deleteResturant(id){
            let result = await axios.delete('http://localhost:3000/restaurant/'+id)
            console.log(result)
            if(result.status==200){
                alert("Restaurant deleted successfully")
                this.loadData();
                this.$router.push({name:"Add"})
            }
        },
        async loadData()
        {
          let user=localStorage.getItem('user-info');
          if (!user)
          {
            this.$router.push({name:'SignUp'})
          }
          let result = await axios.get('http://localhost:3000/restaurant/')
          console.warn(result)
          this.resturants=result.data
        },
    async addRestaurent()
    {
        let result = await axios.post('http://localhost:3000/restaurant/',{
            name:this.addname,
            address:this.address,
            contact:this.contact
        })
        if (result.status==201){
            alert('Resturant Added Successfully')
            this.loadData();
            this.$router.push({name:"Add"})
        }
    }
    },
    mounted()
{
    this.loadData();
}
}
</script>

<style>
.container-2{
   float: right;
   width:30%;
    border-left: 1px solid;
    
}
.container-1{
    margin-top: 10px;
     
 }

td{
    width: 160px;
    height: 40px;
 }
 
 .btn {
   background-color: #f44336;
   border-radius: 12px;
   margin-left: 2px;
 
 }

 
</style>