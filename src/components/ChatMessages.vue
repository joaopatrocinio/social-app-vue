<template>
    <div class="card" id="chatContainer">
        <div class="card-body">
            <p v-for="msg of messages" :key="msg._id" class="m-0">
                <b>{{ msg.user }}</b>: {{ msg.message }}
            </p>
        </div>
    </div>  
</template>

<script>
import Vue from 'vue'
export default {
    name: "ChatMessages",
    props: ["messages"],
    watch: {
        messages() {
            Vue.nextTick(() => {
                document.getElementById("chatContainer").scrollTop = document.getElementById("chatContainer").scrollHeight;
            });
        }
    }
}
</script>

<style scoped>
#chatContainer {
    overflow-y: scroll;
    height: 400px;
}
</style>