<template>
    <div class="card-register">
        <img class="logo" src="../assets/logo.png" alt="Logo">
        <h1>Sign Up</h1>
        <div class="register">
            <input type="text" v-model="name" placeholder="Name" required>
            <input type="email" v-model="email" placeholder="Email" required>
            <input type="password" v-model="password" placeholder="Password" required>
            <button v-on:click="signUp">Sign Up</button>
        </div>
        <router-link to="/login" class="button-register">Already have an account?</router-link>
    </div>
</template>

<script>
import axios from 'axios';
    export default {
        name:'SignUp',
        data() {
            return {
                name: '',
                email: '',
                password: ''
            }
        },
        methods: {
            async signUp() {
                let result = await axios.post("http://localhost:3000/user",{
                    email: this.email,
                    password: this.password,
                    name: this.name,
                });

                if (result.status == 201)
                {
                    localStorage.setItem('user-info', JSON.stringify(result))
                    this.$router.push({name:"Home"})
                }
            },
            login() {
                this.$router.push({name: "Login"})
            }
        },
        mounted() {
            let user = localStorage.getItem('user-info');
            if(user) {
                this.$router.push({name: "Home"})
            }
        }
    }
</script>