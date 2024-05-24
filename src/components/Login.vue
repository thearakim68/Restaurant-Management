<template>
    <div class="card-register">
        <img class="logo" src="../assets/logo.png" alt="Logo">
        <h1>Login</h1>
        <div class="login">
            <div class="email">
                <input type="email" v-model="email" placeholder="Email" required>
                <p v-if="emailError" class="error-message">{{ emailError }}</p>
            </div>
            <div class="password">
                <input type="password" v-model="password" placeholder="Password" required>
                <p v-if="passwordError" class="error-message">{{ passwordError }}</p>
            </div>
            <button v-on:click="login">Login</button>
            <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        </div>
        <router-link to="/sign-up" class="button-register">Don't have an account yet?</router-link>
    </div>
</template>

<script>
import axios from 'axios'; // Importing axios for HTTP requests

export default {
    name: "Login", // Name of the component
    data() {
        return {
            email: "", // Model for the email input
            password: "", // Model for the password input
            errorMessage: "", // Error message for general login errors
            emailError: "", // Error message for email validation
            passwordError: "", // Error message for password validation
        }
    },
    methods: {
        // Method to handle the login action
        async login() {
            // Reset all error messages
            this.emailError = "";
            this.passwordError = "";
            this.errorMessage = "";

            // Validate email and password fields
            if (!this.email) {
                this.emailError = "Please enter your email.";
            }
            if (!this.password) {
                this.passwordError = "Please enter your password.";
            }

            // If there are validation errors, do not proceed
            if (this.emailError || this.passwordError) {
                return;
            }

            try {
                // Send a GET request to the server to check the user credentials
                const result = await axios.get(
                    `http://localhost:3000/user?email=${this.email}&password=${this.password}`
                );

                // Check if the response is successful and contains user data
                if (result.status === 200 && result.data.length > 0) {
                    // Store user information in localStorage
                    localStorage.setItem("user-info", JSON.stringify(result.data[0]));
                    // Redirect to the Home page
                    this.$router.push({ name: "Home" });
                } else {
                    // Set an error message if the credentials are invalid
                    this.errorMessage = "Invalid credentials. Please try again.";
                }
            } catch (error) {
                // Log the error and set a general error message
                console.error("Error logging in:", error);
                this.errorMessage = "An error occurred. Please try again later.";
            }
        }
    },
    // Lifecycle hook to check if the user is already logged in
    mounted() {
        const user = localStorage.getItem("user-info");
        if (user) {
            this.$router.push({ name: "Home" });
        }
    }
}
</script>

<style scoped>
.error-message {
    color: red; /* Set error message color to red */
    float: left; /* Float error message to the left */
}

.email .error-message, .password .error-message {
    margin-top: -10px; /* Adjust margin for email and password error messages */
}
</style>
