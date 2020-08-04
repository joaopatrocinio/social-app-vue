<template>
    <div class="card">
        <div class="card-body">
            <p v-for="msg of messages" :key="msg._id" class="m-0">
                <b>{{ msg.user }}</b>: {{ msg.message }}
            </p>
        </div>
    </div>  
</template>

<script>
export default {
    name: "ChatMessages",
    props: ["messages"]
}
</script>