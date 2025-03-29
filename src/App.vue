<template>
  <div class="contenedor">
    <h1>Sistema de Aseguradora</h1>

    <!-- Formulario para registrar pólizas -->
    <FormularioPoliza />

    <!-- Tabla para mostrar pólizas -->
    <ListaPolizas />
  </div>
</template>

<script>
import FormularioPoliza from './components/FormularioPoliza.vue';
import ListaPolizas from './components/ListaPolizas.vue';

export default {
  components: {
    FormularioPoliza,
    ListaPolizas,
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  background-color: #f1f5f9;
}

.contenedor {
  padding: 40px 20px;
}

h1 {
  text-align: center;
  font-size: 36px;
  color: #1e3a8a;
  margin-bottom: 40px;
}
</style>
