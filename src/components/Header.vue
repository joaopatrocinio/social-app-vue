<template>
    <b-navbar toggleable="lg" type="dark" variant="info" class="mb-4">
        <b-navbar-brand href="/">Social App</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
                <b-nav-item>
                    <router-link class="nav-link" to="/">Home</router-link>
                </b-nav-item>
                <b-nav-item v-if="loggedIn">
                    <router-link class="nav-link" to="/chat">Chat</router-link>
                </b-nav-item>
                <b-nav-item>
                    <router-link class="nav-link" to="/about">About</router-link>
                </b-nav-item>
            </b-navbar-nav>

            <b-navbar-nav class="ml-auto">
                <b-nav-item-dropdown right>
                    <template v-slot:button-content>
                        <span v-if="loggedIn">{{ email }}</span>
                        <span v-else>Not logged in</span>
                    </template>
                    <router-link v-if="!loggedIn" class="dropdown-item" to="/login">Login</router-link>
                    <router-link v-if="!loggedIn" class="dropdown-item" to="/signup">Signup</router-link>
					<a v-else class="dropdown-item" @click="logout">Logout</a>
                </b-nav-item-dropdown>
            </b-navbar-nav>
        </b-collapse>
    </b-navbar>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Header',
    computed: {
        loggedIn() {
            return this.$store.state.auth.loggedIn
        },
        email() {
            return this.$store.state.auth.email
        }
    },
    mounted() {
        axios.get("http://localhost:4060/authentication/verify", {
            withCredentials: true
        }).then((res) => {
            if (res.data.user) {
                this.$store.state.auth.loggedIn = true;
                this.$store.state.auth.email = res.data.user.email;
            }
        })
    },
	methods: {
		logout() {
            axios.get('http://localhost:4060/authentication/logout', { withCredentials: true })
            .then(response => {
                if (response.status == 200) {
                    this.$store.state.auth.loggedIn = false;
                    this.$store.state.auth.email = "";
                    this.$router.push("/");
                } else {
                    alert("Erro")
                }
            });
		}
	}
}
</script>

<style scoped>
a,
a:hover {
	color: inherit;
	text-decoration: none;
	cursor: pointer;
}
</style>