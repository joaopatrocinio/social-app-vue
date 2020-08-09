<template>
	<div>
		<h1>Search Result</h1>
		<div class="d-flex">
			<PersonCard class="m-2" v-bind:person="person" v-for="person in searchResult" :key="person._id"></PersonCard>
		</div>
	</div>
</template>

<script>
import axios from 'axios'
import PersonCard from '@/components/PersonCard.vue'
export default {
	name: "Search",
	components: {
		PersonCard
	},
	data() {
		return {
			searchResult: {}
		}
	},
	computed: {
		searchText() {
			return this.$route.params.query
		}
	},
	watch: {
		searchText() {
			axios
			.get("http://localhost:4060/people/search/" + this.searchText)
			.then(result => {
				console.log(result.data)
				this.searchResult = result.data;
			})
		}
	}
}
</script>