<template>
  <div>
    <input v-model="message" type="text" name="" id="" placeholder="send a message">
    <button @click="send" type="submit">send message</button>
    <p>the response from the server is: {{response}}</p>
    <p>this is the websocket object {{this.connection.protocol}}</p>
  </div>
</template>

<script>
export default {
  name: 'websocket',
data(){
  return{
    message: '',
    response: '',
    connection: null
  }
},
  methods:{
        send(){
      console.log(this.connection);
      this.connection.send(this.message)
    }
  },
  created: function(){
    console.log('starting Connection to websocket')
    this.connection = new WebSocket("ws://127.0.0.1:5436")
    // this.connection = new WebSocket("wss://echo.websocket.org");

    this.connection.onopen = event =>{
      console.log(event);
      console.log('a connection has been established')
    }

    this.connection.onerror = error =>{
      console.log(`WebSocket error: ${error}`)
    }

    this.connection.onmessage = event => {
      this.response = event.data;
      console.log(event);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
