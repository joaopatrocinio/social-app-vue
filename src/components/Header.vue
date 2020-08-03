<template>
    <b-navbar toggleable="lg" type="dark" variant="info" class="mb-4">
        <b-navbar-brand href="/">Social App</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
                <b-nav-item>
                    <router-link class="nav-link" to="/">Home</router-link>
                </b-nav-item>
                <b-nav-item>
                    <router-link class="nav-link" to="/about">About</router-link>
                </b-nav-item>
            </b-navbar-nav>

            <b-navbar-nav class="ml-auto">
                <b-nav-item-dropdown right>
                    <template v-slot:button-content>
                        <span v-if="loggedIn">Logged in</span>
                        <span v-else>Not logged in</span>
                    </template>
                    <router-link class="dropdown-item" to="/login">Login</router-link>
                    <router-link class="dropdown-item" to="/signup">Signup</router-link>
                </b-nav-item-dropdown>
            </b-navbar-nav>
        </b-collapse>
    </b-navbar>
</template>

<script>
export default {
    name: 'Header',
    props: ["loggedIn"],
    data: function () {
        return {
            email: ""
        }
    }
}
</script>

<style scoped>
a,
a:hover {
	color: inherit;
	text-decoration: none;
}
</style>