<template>
  <div class="card">
    <div class="card-header pb-0 px-3">
      <h6 class="mb-0">User Information</h6>
    </div>
    <div class="card-body pt-4 p-3">
      <ul v-if="posts && posts.length" class="list-group">
        <li v-for="p in posts" class="list-group-item border-0 d-flex p-4 mb-2 bg-gray-100 border-radius-lg">
          <img :src="p.avatar"/>
          <div class="d-flex flex-column">
            <h6 class="mb-3 text-sm">{{ p.first_name}} {{ p.last_name}}</h6>
            <span class="mb-2 text-xs">
              Company Name:
              <span class="text-dark font-weight-bold ms-sm-2">Stechoq</span>
            </span>
            <span class="mb-2 text-xs">
              Email Address:
              <span class="text-dark ms-sm-2 font-weight-bold">{{ p.email}}</span>
            </span>
          </div>
          <div class="ms-auto text-end">
            <a class="btn btn-link text-danger text-gradient px-3 mb-0" href="javascript:;">
              <i class="far fa-trash-alt me-2" aria-hidden="true"></i>Delete
            </a>
            <a class="btn btn-link text-dark px-3 mb-0" href="../signin">
              <i class="fas fa-pencil-alt text-dark me-2" aria-hidden="true"></i>Edit
            </a>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  export default {
    name: "table",
    data() {
      return {
        posts: [],
        errors: []
      };
    },
    async created() {
      try {
        const response = await axios.get(`https://reqres.in/api/users?page=2`);
        this.posts = response.data.data;
      }
      catch (e) {
        this.errors.push(e);
      }
    },
    
    methods: {
      remove() {
        axios.delete(`https://reqres.in/api/users/2`)
          .then(response => {
            console.log(response);
            alert(response.status + " User deleted")
          })
          .catch(e => {
            this.errors.push(e);
          });
      }
    }
  };
  </script>
