<template>
  <Header />    
  <h1>RESTAURANT MANAGEMENT</h1>
  <!-- <table border="1">
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
</table> -->
  </template>


  <script>
  import axios from 'axios'
import Header from './Header.vue'
export default{
    name:'Home',
    data()
    {
      return{
        name:'',
        resturants:[],
      }

    },
    components:{
      Header
    },
    methods: {
        async deleteResturant(id){
            let result = await axios.delete('http://localhost:3000/restaurant/'+id)
            console.log(result)
            if(result.status==200){
                alert("Restaurant deleted successfully")
                this.loadData();
                this.$router.push({name:"Home"})
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
        }
      }, 
    async mounted()
  {
    this.loadData();
  }
}
</script>

<style>
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