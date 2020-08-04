<template>
    <div>
        <h1>Chat</h1>
        <ChatMessages v-bind:messages="messages"></ChatMessages>
        <b-row class="mt-2">
            <b-col cols="10">
                <b-form-input type="text" v-model="sendText" placeholder="Type to chat..."></b-form-input>
            </b-col>
            <b-col cols="2">
                <b-button class="btn-block" variant="primary" v-on:click="sendMessage">Send</b-button>
            </b-col>
        </b-row>
    </div>
</template>

<script>
import ChatMessages from '@/components/ChatMessages.vue'
export default {
    name: "Chat",
    components: {
        ChatMessages
    },
    data() {
        return {
            sendText: "",
            messages: []
        }
    },
    sockets: {
        previousMessages(data) {
            for (let msg of data) {
                this.messages.push({
                    user: msg.user,
                    message: msg.message
                })
            }
        },
        chatMessage(data) {
            this.messages.push({
                user: data.user,
                message: data.message
            })
        }
    },
    created() {
        if (!this.$store.state.auth.loggedIn) {
            this.$router.push("/login")
        }
    },
    mounted() {
        this.$socket.emit("chat connect");
    },
    methods: {
        sendMessage() {
            this.$socket.emit("chatMessage", this.sendText);
            this.sendText = "";
        }
    }
}
</script>