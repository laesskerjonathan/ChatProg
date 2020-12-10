<template>
  <MainChat class="main-chat" v-bind:messages="messages"/>
  <form v-on:submit.prevent="submitForm">
      <textarea v-model="text"></textarea>
      <button type="submit">Senden</button>
  </form>
</template>

<script>
import MainChat from './components/MainChat';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    MainChat
  },
  created() {
      axios.get('https://l2b5tgsdwl.execute-api.us-east-2.amazonaws.com/live4/message')
        .then((res) => {
          this.messages = res.data.Items;
            console.log(res);
        })
        .catch((error) => {
            console.error(error);
        })
  },
  data() {
    return {
      messages: [
      ],
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
                this.messages.push({id: {S: maxId.toString()}, message: {S: this.text}, timestamp: {N: Date.now()}});
            })
            .catch((error) => {
                console.error(error);
            })
            
      }
  }
}
</script>


<style>
   body {
     background-color: black;
   }

   main-chat {
     height: 100px;
     max-height: 100px;
     display: block;
     overflow: scroll;
   }
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
