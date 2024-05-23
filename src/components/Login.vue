<template>
    <div class="card-register">
        <img class="logo" src="../assets/logo.png" alt="Logo">
        <h1>Login</h1>
        <div class="login">
            <input type="email" v-model="email" placeholder="Email" required>
            <input type="password" v-model="password" placeholder="Password" required>
            <button v-on:click="login">Login</button>
        </div>
        <router-link to="/sign-up" class="button-register">Don't have an account yet?</router-link>
    </div>
</template>

<script>
import axios from 'axios';
    export default {
        name: "Login",
        data() {
            return{
                email: "",
                password: ""
            }
        },
        methods: {
            async login() {
                let result = await axios.get(
                    `http://localhost:3000/user?email=${this.email}&password=${this.password}`
                );
                if(result.status==200 && result.data.length>0)
                {
                    localStorage.setItem("user-info", JSON.stringify(result.data[0]))
                    this.$router.push({name: "Home"})
                }
            }
        },
        mounted()
        {
            let user = localStorage.getItem("user-info");
            if(user)
            {
                this.$router.push({name:"Home"})
            }
        }
    }
</script>