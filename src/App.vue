<template>
  <div id="app">
    <FormularioCliente />
  </div>
</template>

<script>
import FormularioCliente from './components/FormularioCliente.vue';

export default {
  name: 'App',
  components: {
    FormularioCliente,
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 50px;
}
</style>
