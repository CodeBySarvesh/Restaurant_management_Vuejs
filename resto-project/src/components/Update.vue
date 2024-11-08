<template>
    <Header />
    <h1>Update Restaurant</h1>
    <div class="update">
        <input type="text" name="name" placeholder="Enter Restaurent Name" v-model="restaurant.name" />
        <input type="text" name="address" placeholder="Enter Restaurent Address" v-model="restaurant.address" />
        <input type="text" name="contact" placeholder="Enter Restaurent Contect" v-model="restaurant.contact" />
        <button type="button" v-on:click="updateRestaurent">
            Update Restaurant
        </button>
    </div>
</template>

<script>
import axios from 'axios'
import Header from "./Header.vue";
export default {
    name: "Update",
    components: {
        Header,
    },
    data() {
        return {
            restaurant: {
                name: '',
                address: '',
                contact: ''
            },
        };
    },
    methods:{
        async updateRestaurent(){
            let result = await axios.put('http://localhost:3000/restaurant/'+this.$route.params.id, {
                name:this.restaurant.name,
                address:this.restaurant.address,
                contact:this.restaurant.contact
            })

            if(result.status==200){
                this.$router.push({name:"Add"})
            }
        }
    },
    async mounted() {
        let user = localStorage.getItem("user-info");
        if (!user) {
            this.$router.push({ name: "SignUp" });
        }
        const result = await axios.get('http://localhost:3000/restaurant/' + this.$route.params.id)
        this.restaurant = result.data
    },
};
</script>
