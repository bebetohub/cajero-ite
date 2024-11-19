<template>
    <div>
      <h2>VER SALDO</h2>
      <p v-if="cuenta">Saldo actual: {{ cuenta.balance }}</p>
      <p v-else>No se ha encontrado la cuenta</p>
      <button @click="$emit('volver')">Volver al menú</button>
    </div>
  </template>
  
  <script>
  export default {
  props: {
    cuenta: Object
  },
  watch: {
    cuenta(newValue) {
      console.log(newValue);
    }
  }
}
  </script>