<script>
import ChatCard from './ChatCard.vue';
import ChatMessage from './ChatMessage.vue';
import axios from 'axios';

export default {
  name: 'ChatComponent',
  components: {
    ChatCard,
    ChatMessage
  },
  data() {
    return {
      userLeft: {},
      userRight: {},
      messages: []
    };
  },
  async created() {
    try {
      const url = 'https://randomuser.me/api/?results=2';
      const { data } = await axios.get(url);

      // Se asignan los usuarios a los lados correspondientes
      this.userLeft = { ...data.results[0], side: 'left' };
      this.userRight = { ...data.results[1], side: 'right' };
    } catch (error) {
      console.error('Error al obtener los usuarios:', error);
    }
  },
  methods: {
    enviarMensaje(message, color, name, side) {
      // Se agrega el mensaje enviado al array de mensajes
      this.messages.push({ message, color, name, side });
    }
  }
};
</script>

<template>
  <div class="row chat-container">
    <!-- Tarjeta del usuario izquierdo -->
    <ChatCard :user="userLeft" @enviar-mensaje="enviarMensaje" v-if="Object.keys(userLeft).length > 0" />

    <!-- Contenedor de los mensajes del chat -->
    <ChatMessage :messages="messages" />

    <!-- Tarjeta del usuario derecho -->
    <ChatCard :user="userRight" @enviar-mensaje="enviarMensaje" v-if="Object.keys(userRight).length > 0" />
  </div>
</template>

<style scoped>
.chat-container {
  display: flex;
  justify-content: space-between;
}

.row {
  gap: 20px;
  /* Espacio entre las columnas */
}
</style>
