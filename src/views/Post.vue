<template>
    <div>
        <div class="user-add">
            <h2>Add user</h2>
            <input type="text" v-model="name" /> <br />
            <input type="text" v-model="email" /> <br />

            <button @click="storeUser">Store</button>
        </div>

    </div>
</template>

<script>
import axios from "axios";
export default {
    name: "App",
    data() {
        return {
            email: '',
            name: '',
        };
    },
    methods: {
        async storeUser() {
            try {
                const user = await axios.post(
                    "https://reqres.in/api/users",
                    {
                        name: this.name,
                        job: this.email
                    }
                );

                console.log(user)
            } catch (e) {
                console.log(e);
            }
        },
    }
}
</script>