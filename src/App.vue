<template>
  <router-view />
</template>

<script>

export default {
  name: 'App',
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  padding: 0;
  margin: 0;
}
.card-register {
    width: 300px;
    background-color: #f2f2f2;
    padding: 60px;
    margin-left: auto;
    margin-right: auto;
    margin-top: 90px;
    border-radius: 20px;
    border: solid 1px #d0c9c9;
    align-items: center;
    display: flex;
    flex-direction: column;
    }
    .logo {
        width: 100px;
    }
    input {
        width: 300px;
        height: 40px;
        padding-left: 16px;
        border: solid 1px #f79814;
        border-radius: 4px;
        display: block;
        margin-bottom: 20px;
        margin-left: auto;
        margin-right: auto;
    }
    .card-register button {
        width: 320px;
        height: 44px;
        border-radius: 4px;
        background-color: hsl(43, 100%, 41%);
        box-shadow: 4px 4px 5px hsla(42, 100%, 16%, 0.2);
        border: solid 1px hsl(43, 100%, 41%);
        color: white;
        cursor: pointer;
        /* margin-bottom: 20px; */
    }
    .card-register .button-register {
        margin-top: 20px;
    }
</style>
