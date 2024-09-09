<template>
  <h1>Chat App</h1>
  <div class="chat-app-container container">
    <ChatComponent />
  </div>
</template>

<script>
import ChatComponent from './components/ChatComponent.vue';

export default {
  name: 'App',
  components: {
    ChatComponent
  }
};
</script>

<style>
.chat-app-container {
  margin-top: 20px;
}

h1 {
  text-align: center;
}
</style>
