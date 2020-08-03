<template>
	<div id="app">
		<Header v-bind:loggedIn=loggedIn></Header>
		<router-view @loggedIn="setLoggedIn" class="container"></router-view>
	</div>
</template>

<script>
import Header from '@/components/Header.vue'
export default {
	components: {
		Header
	},
	data: function() {
		return {
			loggedIn: false
		}
	},
	methods: {
		setLoggedIn(status) {
			this.loggedIn = status;
		}
    }
}
</script>