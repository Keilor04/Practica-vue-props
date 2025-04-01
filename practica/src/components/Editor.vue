<template>
  <div>
    <hr>
    <h3>{{ tituloeditor }}</h3>
    <div>
    <input type="text" :value="mensajeescrito" v-on:input="actualizarmensajeescrito" v-on:keyup.enter="enviarmensaje">
    <button v-on:click="enviarmensaje">Enviar mensaje</button>
  </div>
    <button v-on:click="emitirEvento">Mostrar mensaje en componente vista</button>
    <hr> 
  </div>
</template>

<script>
export default {
  //Props sirve para recibir datos del componente Padre
  props: {
    textoAEditar: {
      type: String, //string porque se recibe texto del componente Padre
    },
    
  },

  data() {
    return {
      mensajeescrito: '',
      tituloeditor: 'Componente hijo-->Editor',
    }
  },
  methods: {
    //emitirEvento sirve para emitir un evento al componente padre
    //para que el padre pueda recibir el evento y mostrarlo en el hijo vista
    //en este caso se emite el evento Mostrarsaludo
    emitirEvento() {
      this.$emit('Mostrarsaludo') // Emitimos el evento con un dato
    },

    actualizarmensajeescrito(event) {
      this.mensajeescrito = event.target.value; // evento.target.value es el valor del input
    },
    enviarmensaje() {
      if (this.mensajeescrito.trim() !== '') {
        this.$emit('mensaje-escrito', this.mensajeescrito);
        this.mensajeescrito = ''; // Limpiar el input después de enviar
      }
    }
  },
}
</script>



<style scoped>
.item {
  margin-top: 2rem;
  display: flex;
  position: relative;
}

.details {
  flex: 1;
  margin-left: 1rem;
}

i {
  display: flex;
  place-items: center;
  place-content: center;
  width: 32px;
  height: 32px;
  color: var(--color-text);
}

h3 {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: var(--color-heading);
}

@media (min-width: 1024px) {
  .item {
    margin-top: 0;
    padding: 0.4rem 0 1rem calc(var(--section-gap) / 2);
  }

  i {
    top: calc(50% - 25px);
    left: -26px;
    position: absolute;
    border: 1px solid var(--color-border);
    background: var(--color-background);
    border-radius: 8px;
    width: 50px;
    height: 50px;
  }

  .item:before {
    content: ' ';
    border-left: 1px solid var(--color-border);
    position: absolute;
    left: 0;
    bottom: calc(50% + 25px);
    height: calc(50% - 25px);
  }

  .item:after {
    content: ' ';
    border-left: 1px solid var(--color-border);
    position: absolute;
    left: 0;
    top: calc(50% + 25px);
    height: calc(50% - 25px);
  }

  .item:first-of-type:before {
    display: none;
  }

  .item:last-of-type:after {
    display: none;
  }
}
</style>
