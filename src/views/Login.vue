<template>
    <div class="login-container">
        <b-form @submit="login">
            <b-form-group id="input-group-email" label="Email address:" label-for="email">
                <b-form-input id="email" v-model="form.email" type="email" required placeholder="Enter email" ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-password" label="Password" label-for="input-2">
                <b-form-input id="input-2" v-model="form.password" type="password" required placeholder="Enter password" ></b-form-input>
            </b-form-group>

            <b-button type="submit" variant="primary">Submit</b-button>
        </b-form>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Login',
    data() {
        return {
            form: {
                email: "",
                password: ""
            },
        }
    },
    methods: {
        login: function (event) {
            event.preventDefault();
            axios.post('http://localhost:4060/authentication/login', {
                email: this.form.email,
                password: this.form.password
            }).then(response => {
                if (response.status == 200) {
                    this.$store.commit("setLoggedIn", true)
                    this.$store.commit("setEmail", response.data.user.email)
                    this.$router.push("/")
                } else {
                    alert("Login errado.")
                }
            });
        }
    }
}
</script>
