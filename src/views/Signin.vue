<template>
  <div class="container top-0 position-sticky z-index-sticky">
    <div class="row">
      <div class="col-12">
        <navbar
          isBlur="blur  border-radius-lg my-3 py-2 start-0 end-0 mx-4 shadow"
          v-bind:darkMode="true"
          isBtn="bg-gradient-success"
        />
      </div>
    </div>
  </div>
  <main class="mt-0 main-content">
    <section>
      <div class="page-header min-vh-100">
        <div class="container">
          <div class="row">
            <div class="mx-auto col-xl-4 col-lg-5 col-md-7 d-flex flex-column mx-lg-0">
              <div class="card card-plain">
                <div class="pb-0 card-header text-start">
                  <h4 class="font-weight-bolder">Edit</h4>
                  <p class="mb-0">Enter your Edit Data</p>
                </div>
                <div class="card-body">
    
                    <div class="mb-3">
                      <argon-input type="email" placeholder="Email" name="email" size="lg" v-model="email" />
                    </div>
                    <div class="mb-3">
                      <argon-input type="text" placeholder="fiirt_name" name="first_name" size="lg" v-model="first_name" />
                    </div>

                    <div class="text-center">
                      <argon-button
                        class="mt-4"
                        variant="gradient"
                        color="success"
                        fullWidth
                        size="lg"
                        @click="save"
                      >Sign in</argon-button>
                    </div>
                
                </div>
                <div class="px-1 pt-0 text-center card-footer px-lg-2">
                  <p class="mx-auto mb-4 text-sm">
                    Don't have an account?
                    <a
                      href="javascript:;"
                      class="text-success text-gradient font-weight-bold"
                    >Save</a>
                  </p>
                </div>
              </div>
            </div>
            <div
              class="top-0 my-auto text-center col-6 d-lg-flex d-none h-100 pe-0 position-absolute end-0 justify-content-center flex-column"
            >
              <div
                class="position-relative bg-gradient-primary h-100 m-3 px-7 border-radius-lg d-flex flex-column justify-content-center overflow-hidden"
                style="background-image: url('https://raw.githubusercontent.com/creativetimofficial/public-assets/master/argon-dashboard-pro/assets/img/signin-ill.jpg');
          background-size: cover;"
              >
                <span class="mask bg-gradient-success opacity-6"></span>
                <h4
                  class="mt-5 text-white font-weight-bolder position-relative"
                >"Attention is the new currency"</h4>
                <p
                  class="text-white position-relative"
                >The more effortless the writing looks, the more effort the writer actually put into the process.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
  import ArgonInput from "@/components/ArgonInput.vue";
  import ArgonButton from "@/components/ArgonButton.vue";
  import axios from 'axios';
  const body = document.getElementsByTagName("body")[0];
  export default {
    name: "profile",
    data() {
      return {
        showMenu: false,
        errors: [],
        author: '',
        email: '',
        first_name: '',
        last_name: ''
      };
    },
    async created() {
      try {
        const response = await axios.get(`https://reqres.in/api/users/2`)
        this.author = response.data.data
        this.email = this.author.email
        this.first_name = this.author.first_name
        this.last_name = this.author.last_name
      } catch (e) {
        this.errors.push(e)
      }
    },
    methods: {
      save() {
        axios.put(`https://reqres.in/api/users/2`, {
          email: this.email,
          first_name: this.first_name,
          last_name: this.last_name
        })
          .then(response => {
            console.log(response)
            alert(response.status + " User updated")
            this.author.email = this.email
            this.author.first_name = this.first_name
            this.author.last_name = this.last_name
          })
          .catch(e => {
            this.errors.push(e)
          })
      }
    },
    components: { ArgonInput, ArgonButton },
    beforeMount() {
      this.$store.state.imageLayout = "profile-overview";
      this.$store.state.showNavbar = false;
      this.$store.state.showFooter = true;
      this.$store.state.hideConfigButton = true;
      body.classList.add("profile-overview");
    },
    beforeUnmount() {
      this.$store.state.isAbsolute = false;
      this.$store.state.imageLayout = "default";
      this.$store.state.showNavbar = true;
      this.$store.state.showFooter = true;
      this.$store.state.hideConfigButton = false;
      body.classList.remove("profile-overview");
    }
  };
  </script>