<template>
    <div class="tabla">
      <h2>Listado de Pólizas</h2>
  
      <table v-if="polizas.length > 0">
        <thead>
          <tr>
            <th>Número</th>
            <th>Tipo</th>
            <th>Titular</th>
            <th>Monto</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="poliza in polizas" :key="poliza._id">
            <td v-if="editandoId !== poliza._id">{{ poliza.numeroPoliza }}</td>
            <td v-else><input v-model="formEdit.numeroPoliza" /></td>
  
            <td v-if="editandoId !== poliza._id">{{ poliza.tipoSeguro }}</td>
            <td v-else>
              <select v-model="formEdit.tipoSeguro">
                <option>Auto</option>
                <option>Vida</option>
                <option>Hogar</option>
                <option>Salud</option>
              </select>
            </td>
  
            <td v-if="editandoId !== poliza._id">{{ poliza.titular }}</td>
            <td v-else><input v-model="formEdit.titular" /></td>
  
            <td v-if="editandoId !== poliza._id">{{ poliza.monto }}</td>
            <td v-else><input type="number" v-model="formEdit.monto" /></td>
  
            <td>
              <div class="acciones">
                <button v-if="editandoId !== poliza._id" @click="activarEdicion(poliza)">Editar</button>
                <button v-else @click="guardarCambios(poliza._id)">Guardar</button>
                <button @click="eliminarPoliza(poliza._id)" class="eliminar">Eliminar</button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
  
      <p v-else>No hay pólizas registradas.</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        polizas: [],
        editandoId: null,
        formEdit: {
          numeroPoliza: '',
          tipoSeguro: '',
          titular: '',
          monto: null,
        },
      };
    },
    mounted() {
      this.obtenerPolizas();
    },
    methods: {
      async obtenerPolizas() {
        try {
          const res = await axios.get('http://localhost:5000/polizas');
          this.polizas = res.data;
        } catch (error) {
          console.error('Error al obtener pólizas:', error);
        }
      },
      activarEdicion(poliza) {
        this.editandoId = poliza._id;
        this.formEdit = { ...poliza };
      },
      async guardarCambios(id) {
        try {
          await axios.put(`http://localhost:5000/polizas/${id}`, this.formEdit);
          this.editandoId = null;
          this.formEdit = {};
          this.obtenerPolizas();
        } catch (error) {
          console.error('Error al guardar cambios:', error);
        }
      },
      async eliminarPoliza(id) {
        if (confirm("¿Seguro que quiere eliminar esta póliza?")) {
          try {
            await axios.delete(`http://localhost:5000/polizas/${id}`);
            this.obtenerPolizas();
          } catch (error) {
            console.error('Error al eliminar póliza:', error);
          }
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .tabla {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
  }
  
  h2 {
    text-align: center;
    color: #1e3a8a;
    margin-bottom: 20px;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
  }
  
  thead {
    background-color: #2563eb;
    color: white;
  }
  
  th,
  td {
    padding: 12px;
    border: 1px solid #ccc;
    text-align: center;
  }
  
  input,
  select {
    padding: 6px;
    width: 100%;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .acciones {
    display: flex;
    gap: 8px;
    justify-content: center;
  }
  
  button {
    padding: 6px 12px;
    background-color: #2563eb;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #1d4ed8;
  }
  
  button.eliminar {
    background-color: #dc2626;
  }
  
  button.eliminar:hover {
    background-color: #b91c1c;
  }
  </style>
  