<template>
    <div>
      <button @click="getUsers">Get users</button> 
      <div class="users" v-for="user in users" :key="user.id">
        <h2>{{ user.first_name }}</h2>
        <p>{{ user.email }}</p>
      </div>
      </div>
      </template>
  

  <script>
    import axios from "axios";
    export default {
      name: "App",
      data() {
        return {
          users: []
        };
      },
      methods: {
        async getUsers() {
          try {
            const users = await axios.get(
              "https://reqres.in/api/users"
            );
    
            this.users = users.data.data;
          } catch (e) {
            console.log(e);
          }
        },
      },
    };
    </script>