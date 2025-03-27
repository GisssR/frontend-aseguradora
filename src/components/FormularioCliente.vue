<template>
    <div class="formulario">
      <h2>Registrar Cliente</h2>
      <form @submit.prevent="enviarCliente">
        <input v-model="cliente.nombre" placeholder="Nombre" required />
        <input v-model="cliente.email" placeholder="Email" required />
        <button type="submit">Registrar</button>
      </form>
      <p v-if="mensaje">{{ mensaje }}</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        cliente: {
          nombre: '',
          email: '',
        },
        mensaje: '',
      };
    },
    methods: {
      async enviarCliente() {
        try {
          await axios.post('http://localhost:5000/api/clientes', this.cliente);
          this.mensaje = 'Cliente registrado con éxito ✅';
          this.cliente.nombre = '';
          this.cliente.email = '';
        } catch (error) {
          console.error(error);
          this.mensaje = 'Error al registrar cliente 😢';
        }
      },
    },
  };
  </script>
  