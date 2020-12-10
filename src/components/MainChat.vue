<template>
    <div>
        <h1>Chatverlauf {{messages}}</h1>
        
        <div v-bind:key="message.id" v-for="message in messages">
            <Message v-bind:text="message" />
        </div>
    </div>

</template>

<script>
import Message from './Message';

export default {
    name: "MainChat",
    props: ["messages"],
    components: {
        Message
    }
    
}
</script>

<style scoped>
  h1 {
      color: white;
  }

</style>