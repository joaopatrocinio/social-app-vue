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
export default {
    name: 'Login',
    data: function () {
        return {
            form: {
                email: "",
                password: ""
            },
        }
    },
    methods: {
        login: function (event) {
            let self = this;
            event.preventDefault();
            fetch('http://localhost:4060/authentication/login', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    email: this.form.email,
                    password: this.form.password
                })
            }).then(function(response) {
                if (response.status == 200) {
                    console.log(response)
                    self.$emit("loggedIn", true)
                } else {
                    alert("Login errado.")
                }
            });
        }
    }
}
</script>
