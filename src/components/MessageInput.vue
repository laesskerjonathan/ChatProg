<template>
    <div>
        <form v-on:submit.prevent="submitForm">
            <textarea v-model="text"></textarea>
            <button type="submit">Senden</button>
        </form>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        name: "MessageInput",
        props: ["messages"],
        data() {
            return {
                text: ''
            }
        },
        methods: {
            submitForm() {
                var maxId = Math.max.apply(Math, this.messages.map(function(o) {console.log(o.id.S); return o.id.S})) + 1;
                console.log("maxId: ", maxId);
                axios.post('https://l2b5tgsdwl.execute-api.us-east-2.amazonaws.com/live4/message', {
                    id: maxId.toString(),
                    message: this.text
                })
                 .then((res) => {
                     console.log(res);
                     this.messages.push({id: maxId.toString(), message: this.text, timestamp: Date.now()});
                 })
                 .catch((error) => {
                     console.error(error);
                 })
                 
            }
        }
    }
    

</script>

<style scoped>
    textarea {
        display: block;
        margin: 1em auto;
        background-color: blue;
        color: white;
    }
    button {
        margin: 1em auto;
        background-color: red;
    }

</style>