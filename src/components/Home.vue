<template>
    <Header />
    <h1>Hello {{ name }}, Welcome on Homepage</h1>
    <table border="1px">
        <tr>
            <td>ID</td>
            <td>Name</td>
            <td>Contact</td>
            <td>Address</td>
            <td>Action</td>
        </tr>
        <tr v-for="item in restaurant" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.contact }}</td>
            <td>{{ item.address }}</td>
            <td>
                <router-link :to="'/update/'+item.id">Update</router-link>
                <button v-on:click="deleteRestaurant(item.id)">Delete</button>
            </td>
        </tr>
    </table>
</template>

<script>
    import Header from './Header.vue';
    import axios from 'axios';
    export default {
        name: 'Home',
        components: {
            Header
        },
        data() {
            return {
                name: "",
                restaurant: [],
            }
        },
        methods: {
            async deleteRestaurant(id) 
            {
                let result = await axios.delete("http://localhost:3000/restaurant/" + id);
                if(result.status==200)
                {
                    this.loadData();
                }
            },
            async loadData() 
            {
                let user = localStorage.getItem('user-info');
                this.name = JSON.parse(user).name;
                if(!user) 
                {
                    this.$router.push({name: "SignUp"})
                }
                let result = await axios.get("http://localhost:3000/restaurant");
                this.restaurant = result.data;
            }
        },
        async mounted() {
            this.loadData();
        },
    }
</script>

<style>
    table {
        margin: auto;
    }
    td {
        width: 300px;
        height: 40px;
    }
</style>