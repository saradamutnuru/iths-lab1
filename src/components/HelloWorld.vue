<template>
  <div>
    <h1>LAB1 ITHS</h1>
    <div v-for="(message, index) in messages" :key="index">
      {{message.message}}<br>
    </div>
    <button @click="loadMessagesFromBackend()">Reload Message</button>

  <br><br>
  <h2>Post new message:</h2>
  <input type="text" v-model="newMessage">
  <button @click ="postToBackend()">Post</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: function(){
  return{
  messages: [],
  newMessage:''
  }
  },
  methods: {
  loadMessagesFromBackend: function() {
  fetch('http://ec2-3-15-164-37.us-east-2.compute.amazonaws.com:8080/messages')
  .then(response => response.json())
  .then(data => this.messages = data)
},
postToBackend: function(){
  fetch('http://ec2-3-15-164-37.us-east-2.compute.amazonaws.com:8080/message?message='+this.newMessage, {method: 'POSt'})
  .then(response => response.json())
  .then(data => console.log(data))
   this.newMessage='';
}
  }
}
</script>
<style scoped>

</style>
