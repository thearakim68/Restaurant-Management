<template>
    <Header />
    <h1>Welcome to Update Restaurant Page</h1>
    <form action="" class="update">
        <input type="text" name="name" placeholder="Name" v-model="restaurant.name">
        <input type="text" name="address" placeholder="Address" v-model="restaurant.address">
        <input type="text" name="contact" placeholder="Contact" v-model="restaurant.contact">
        <button type="button">Update Restaurant</button>
    </form>
</template>

<script>
    import Header from "./Header.vue"
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
        mounted() {
            let user = localStorage.getItem("user-info");
            if(!user) {
                this.$router.push({name: "SignUp"})
            }
        }
    }
</script>