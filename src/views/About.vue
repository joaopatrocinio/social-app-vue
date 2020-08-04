<template>
	<div class="about">
		<h1>This is an about page</h1>
		<button @click="test++">Check</button>
		<p>Verify auth: {{ verify }}</p>
	</div>
</template>

<script>
import axios from 'axios'
export default {
	name: "About",
	data() {
		return {
			test: 0,
			verify: "Waiting"
		}
	},
	watch: {
		test() {
			axios.get("http://localhost:4060/authentication/verify", {
                withCredentials: true
            }).then((res) => {
				this.verify = res;
			})
		}
	}
}
</script>
