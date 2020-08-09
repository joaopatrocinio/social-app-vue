<template>
    <div>
        <h1>Chat</h1>
        <ChatMessages v-bind:messages="messages"></ChatMessages>
        <form @submit="sendMessage">
            <b-row class="mt-2">
                <b-col cols="10">
                    <b-form-input type="text" class="typingInput" v-model="sendText" placeholder="Type to chat..."></b-form-input>
                </b-col>
                <b-col cols="2">
                    <b-button type="submit" class="btn-block" variant="primary">Send</b-button>
                </b-col>
            </b-row>
        </form>
    </div>
</template>

<script>
import ChatMessages from '@/components/ChatMessages.vue'
import io from 'socket.io-client';

export default {
    name: "Chat",
    components: {
        ChatMessages
    },
    data() {
        return {
            socket: {},
            sendText: "",
            messages: []
        }
    },
    created() {
        if (!this.$store.state.auth.loggedIn) {
            this.$router.push("/login")
        } else {
            this.socket = io("http://localhost:4060");
            this.socket.emit("chatConnect")
        }
    },
    mounted() {
        document.getElementsByClassName("typingInput")[0].focus();
        this.socket.on("previousMessages", (data) => {
            for (let msg of data) {
                this.messages.push({
                    user: msg.user,
                    message: msg.message
                })
            }
        })
        this.socket.on("chatMessage", (data) => {
            this.messages.push({
                user: data.user,
                message: data.message
            })
        })
    },
    destroyed() {
        this.socket.emit("leave");
    },
    methods: {
        sendMessage(e) {
            e.preventDefault();
            this.socket.emit("chatMessage", this.sendText);
            this.sendText = "";
        }
    }
}
</script>