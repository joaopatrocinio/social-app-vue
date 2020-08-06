<template>
    <div>
        <h1 class="mb-4">Signup</h1>
        <b-form @submit="signup">
            <b-form-group id="input-group-email" label="Email address:" label-for="email">
                <b-form-input id="email" v-model="email" type="email" required placeholder="Enter email" ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-password" label="Password" label-for="password">
                <b-form-input id="password" v-model="password" type="password" required placeholder="Enter password" ></b-form-input>
            </b-form-group>

            <b-button type="submit" variant="primary">Create Account</b-button>
        </b-form>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: "Signup",
    data() {
        return {
            email: "",
            password: ""
        }
    },
    methods: {
        signup(event) {
            event.preventDefault();
            axios.post('http://localhost:4060/authentication/signup', {
                email: this.email,
                password: this.password
            }, { withCredentials: true })
            .then(response => {
                if (response.status == 200) {
                    this.$router.push("/login")
                    alert("Account created successfully")
                } else {
                    alert("error")
                }
            });
        }
    }
}
</script>