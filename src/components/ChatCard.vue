<script>
export default {
  name: 'ChatCard',
  data() {
    return {
      message: '',
      color: this.generarColorAleatorio() // Color aleatorio inicial
    };
  },
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  methods: {
    generarColorAleatorio() {
      const letras = '0123456789ABCDEF';
      let color = '#';
      for (let i = 0; i < 6; i++) {
        color += letras[Math.floor(Math.random() * 16)];
      }
      return color;
    },
    enviarMensaje() {

      this.$emit('enviar-mensaje', this.message, this.color, this.user.name.first, this.user.side);
      this.message = '';
      this.color = this.generarColorAleatorio();
    }
  },
  emits: ['enviar-mensaje']
};

</script>

<template>
  <div class="user-component">
    <div class="card">
      <img :src="user.picture.large" class="card-img-top rounded-circle" alt="User Picture" />
      <div class="card-body">
        <h5 class="card-title">{{ user.name.first }} {{ user.name.last }}</h5>
        <form @submit.prevent="enviarMensaje" class="message-form">
          <input v-model="color" type="color" class="form-control" disabled />
          <textarea v-model="message" class="form-control" placeholder="Escribe tu mensaje..."></textarea>

          <div class="btn-container">
            <button type="submit" class="btn-enviar">Enviar</button>
          </div>
        </form>

      </div>
    </div>
  </div>
</template>

<style scoped>
.user-component {
  margin-bottom: 20px;
}

.card {
  box-shadow: 0px 4px 6px 10px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  width: 20rem;

}

.card-body {
  align-items: center;
  text-align: center
}

.rounded-circle {
  border-radius: 8px;
  width: 100px;
  height: 100px;
  object-fit: cover;
  margin: 0 auto;
  display: block;
  padding-top: 20px;
}

textarea {
  width: 90%;
  margin: 10px 0;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

.btn-enviar {
  background-color: #a72c69;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 4px;
  cursor: pointer;
  margin-bottom: 20px;
}

.btn-enviar:hover {
  background-color: #b3004b;
}

.btn-container {
  text-align: center;
}
</style>
