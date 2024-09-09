<script>
export default {
  name: 'ChatMessage',
  props: {
    messages: {
      type: Array,
      required: true
    }
  }
};
</script>

<template>
  <div class="chatbox">
    <div v-for="(message, index) in messages" :key="index" class="message"
      :class="message.side === 'left' ? 'left-message' : 'right-message'">
      <span>{{ message.name }}</span>
      <p class="message-text rounded" :style="{ backgroundColor: message.color }">
        {{ message.message }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.chatbox {
  background-color: #eed9e4;
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 20px;
  width: 80%;
  margin: 0 auto;
}

.message {
  margin-bottom: 10px;
}

.left-message {
  text-align: left;

}

.right-message {
  text-align: right;
}

.message span {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}

.message-text {
  padding: 10px;
  color: white;
  border-radius: 6px;
  word-wrap: break-word;
  max-width: 60%;
  display: inline-block;
}
</style>
