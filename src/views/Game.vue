<template>
	<div>
		<h1 class="mb-4">Game</h1>
		<canvas ref="game" width="600" height="600" style="border:1px solid #000000;"></canvas>
	</div>
</template>

<script>
import io from 'socket.io-client';
export default {
	name: "Game",
	data() {
		return {
			context: {},
			position: {
				x: 0,
				y: 0
			}
		}
	},
	created() {
        if (!this.$store.state.auth.loggedIn) {
            this.$router.push("/login")
        } else {
			this.socket = io("http://localhost:4060");
			this.socket.emit("gameConnect");
        }
    },
	mounted() {
		this.context = this.$refs.game.getContext("2d");
		this.socket.on("position", position => {
			this.position.x = position.x;
			this.position.y = position.y;
			this.context.fillStyle = "#000000";
			this.context.fillRect(this.position.x, this.position.y, 50, 50);
		})
	},
	destroyed() {
        this.socket.emit("leave");
    }
}
</script>

<style scoped>

</style>