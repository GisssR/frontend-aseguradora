<template>
    <div class="formulario">
      <h2>Registrar Póliza</h2>
  
      <form @submit.prevent="registrarPoliza">
        <input v-model="poliza.numeroPoliza" type="text" placeholder="Número de Póliza" required />
        
        <select v-model="poliza.tipoSeguro" required>
          <option disabled value="">Seleccione tipo de seguro</option>
          <option>Auto</option>
          <option>Vida</option>
          <option>Hogar</option>
          <option>Salud</option>
        </select>
        
        <input v-model="poliza.titular" type="text" placeholder="Titular" required />
        <input v-model.number="poliza.monto" type="number" placeholder="Monto" required />
        
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
        poliza: {
          numeroPoliza: '',
          tipoSeguro: '',
          titular: '',
          monto: null,
        },
        mensaje: '',
      };
    },
    methods: {
      async registrarPoliza() {
        try {
        await axios.post('http://localhost:5000/polizas', this.poliza);
          this.mensaje = 'Póliza registrada correctamente ✅';
          this.poliza = {
            numeroPoliza: '',
            tipoSeguro: '',
            titular: '',
            monto: null,
          };
        } catch (error) {
          console.error(error);
          this.mensaje = 'Error al registrar póliza ❌';
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .formulario {
    background-color: #fff;
    max-width: 600px;
    margin: 40px auto;
    padding: 30px;
    border-radius: 16px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  }
  
  .formulario h2 {
    text-align: center;
    color: #1e3a8a;
    font-size: 24px;
    margin-bottom: 24px;
  }
  
  form {
    display: flex;
    flex-direction: column;
    gap: 14px;
  }
  
  input,
  select {
    padding: 10px 14px;
    font-size: 16px;
    border-radius: 8px;
    border: 1px solid #ccc;
    outline-color: #2563eb;
  }
  
  button {
    padding: 12px;
    background-color: #2563eb;
    color: #fff;
    border: none;
    border-radius: 8px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  button:hover {
    background-color: #1d4ed8;
  }
  
  p {
    margin-top: 16px;
    text-align: center;
    font-weight: bold;
    color: green;
  }
  </style>
  