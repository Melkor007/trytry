<template>
  <div class="background">
  </div>
  <div id="aha">
    <img alt="Vue logo" src="./assets/logo.png">
    <ChatBox class="chatbox"></ChatBox>
  </div>
  

</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import ChatBox from './components/ChatBox.vue'

export default {
  name: 'App',
  components: {
    ChatBox
  }
}
</script>

<style>
 html,body{
      margin:0;
      padding:0;
   }
#aha {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width:100%;
  height:100%;
  z-index:1;
}
.background{
  margin: 0;
  z-index:-1;
  background-image:url('./assets/background.jpg');
  background-size:100% 100%;
  width:100%;
  height:100%;
  position:absolute;
}
.chatbox{
  margin-left:30%;
  margin-right:30%
}
</style>
