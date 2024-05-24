<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/add">Add Restaurant</router-link>
        <a v-on:click="logout" href="#">Logout</a>
    </div>
</template>

<script>
    export default {
        name: "Header",
        methods: {
            logout() {
                localStorage.clear();
                this.$router.push({name: "Login"})
            }
        }
    }
</script>

<style>
    .nav {
        background-color: black;
        overflow: hidden;
    }
    .nav a {
        color: white;
        padding: 14px 16px;
        float: left;
        text-align: center;
        font-size: 16px;
        text-decoration: none;
        margin-left: 5px;
    }
    .nav a:hover {
        background-color: #ddd;
        color: #333;
    }
</style>