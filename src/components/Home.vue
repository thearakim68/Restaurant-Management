<template>
    <Header />
    <h1>Hello {{ name }}, Welcome on Homepage</h1>
</template>

<script>
    import Header from './Header.vue';
    export default {
        name: 'Home',
        components: {
            Header
        },
        data() {
            return {
                name: ""
            }
        },
        mounted() {
            let user = localStorage.getItem('user-info');
            this.name = JSON.parse(user).name;
            if(!user) {
                this.$router.push({name: "SignUp"})
            }
        }
    }
</script>

<style>

</style>