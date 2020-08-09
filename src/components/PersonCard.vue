<template>
	<div>
		<b-card 
			v-bind:title="person.email"
			img-src="/default_profile.jpg"
			img-top
		>
			<b-card-text>
				This is a person's profile.
			</b-card-text>
			<b-button href="#" variant="primary">Send friend request</b-button>
		</b-card>
	</div>
</template>

<script>
export default {
	name: "PersonCard",
	props: ["person"]
}
</script>

<style scoped>
.card {
	width: 250px;
}
</style>