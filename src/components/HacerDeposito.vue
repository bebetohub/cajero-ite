<template>
    <template>
  <div>
    <h2>Realizar Depósito</h2>
    <form @submit.prevent="realizarDeposito">
      <label>Monto:</label>
      <input type="number" v-model="monto" />
      <button type="submit">Depositar</button>
    </form>
  </div>
</template>
  </template>
  
  <script>
  export default {
    props: {
      cuenta: Object
    },
    data() {
      return {
        monto: 0
      }
    },
    methods: {
        realizarDeposito() {
      // Lógica para realizar el depósito
      // Actualiza el saldo de la cuenta
      this.$emit('actualizar-saldo', this.monto) // Emite un evento
      //this.cuenta.balance += this.monto
      // Emite un evento para notificar que se realizó el depósito
      this.$emit('deposito-realizado')
    },
    }
  }
  </script>