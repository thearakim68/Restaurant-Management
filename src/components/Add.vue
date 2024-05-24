
<template>
    <Header />
    <h1>Welcome to Add Restaurant Page</h1>
    <form action="" class="add">
        <input type="text" name="name" placeholder="Name" v-model="restaurant.name">
        <input type="text" name="address" placeholder="address" v-model="restaurant.address">
        <input type="text" name="contact" placeholder="contact" v-model="restaurant.contact">
        <button type="button" v-on:click="addRestaurant">Add New Restaurant</button>
    </form>
</template>
<script>
    import Header from "./Header.vue"
      export default {
          name: "Add",
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
            addRestaurant()
                {
                    console.warn(this.restaurant)
                }
          },
          mounted() {
              let user = localStorage.getItem("user-info");
              if (!user) {
                  this.$router.push({name: "SignUp"})
              }
          }
      }
</script>