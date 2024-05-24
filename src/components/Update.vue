<template>
    <Header />
    <h1>Welcome to Update Restaurant Page</h1>
    <form action="" class="update">
        <input type="text" name="name" placeholder="Name" v-model="restaurant.name">
        <input type="text" name="address" placeholder="Address" v-model="restaurant.address">
        <input type="text" name="contact" placeholder="Contact" v-model="restaurant.contact">
        <button type="button" v-on:click="updateRestaurant">Update Restaurant</button>
    </form>
</template>

<script>
    import Header from "./Header.vue";
    import axios from "axios";
    export default {
        name: "Update",
        components: {
            Header
        },
        data() {
            return {
                restaurant: {
                    name: "",
                    address: "",
                    contact: ""
                }
            }
        },
        methods: {
            async updateRestaurant() 
            {
                let result = await axios.put("http://localhost:3000/restaurant/"+this.$route.params.id, {
                    name: this.restaurant.name,
                    address: this.restaurant.address,
                    contact: this.restaurant.contact
                });
                if (result.status == 200)
                {
                    this.$router.push({name: "Home"})
                }
            }
        },
        async mounted() {
            let user = localStorage.getItem("user-info");
            if(!user) {
                this.$router.push({name: "SignUp"})
            }

            const result = await axios.get("http://localhost:3000/restaurant/" + this.$route.params.id);
            this.restaurant = result.data
        }
    }
</script>