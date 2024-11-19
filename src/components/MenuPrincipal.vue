<template>
    <div v-if="!verSaldo">
      <h2>MENU DE OPCIONES</h2>
      <ul>
        <li><button @click="verificarSaldo">Verificar Saldo</button></li><br>
        <li><button @click="realizarDeposito">Realizar Deposito</button></li><br>
        <li><button @click="realizarRetiro">Realizar Retiro</button></li><br>
      </ul>
      
    </div>
    <VerSaldo v-if="verSaldo" :cuenta="cuentaactual" @volver="verSaldo = false"/>
    <HacerDeposito v-if="realizarDepositoVisible" :cuenta="cuentaactual" @actualizar-saldo="actualizarSaldo($event)" @deposito-realizado="realizarDepositoVisible = false"/>
  </template>
  
  <script>
  import VerSaldo from './VerSaldo.vue';
  import HacerDeposito from './HacerDeposito.vue';
  
  export default {
    props: {
      cuentaactual: Object

    },
    
    components: {
      VerSaldo,
      HacerDeposito
    },
    data() {
      return {
        verSaldo: false,
        realizarDepositoVisible: false
      }
    },
    methods: {
      verificarSaldo() {
        console.log(this.cuentaactual);
        this.verSaldo = true;
      },
      realizarDeposito() {
        this.realizarDepositoVisible = true;
      },
      realizarRetiro() {
        // Lógica para realizar retiro
      },
      actualizarSaldo(monto) {
        this.$emit('actualizar-saldo', monto)
      }
    }
  }
  </script>