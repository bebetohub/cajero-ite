<template>
  <div class="menu" v-if="!verSaldo && !realizarDepositoVisible && !realizarRetiroVisible">
    <h2>📋 Menú de Opciones</h2>
    <ul>
      <li>
        <button class="menu-button" @click="verificarSaldo">💰 Verificar Saldo</button>
      </li>
      <li>
        <button class="menu-button" @click="realizarDeposito">➕ Realizar Depósito</button>
      </li>
      <li>
        <button class="menu-button" @click="realizarRetiro">➖ Realizar Retiro</button>
      </li>
    </ul>
  </div>

  <VerSaldo v-if="verSaldo" :cuenta="cuentaactual" @volver="verSaldo = false" />
  <HacerDeposito
    v-if="realizarDepositoVisible"
    :cuenta="cuentaactual"
    @actualizar-saldo="actualizarSaldo($event)"
    @deposito-realizado="realizarDepositoVisible = false"
  />
  <HacerRetiro
    v-if="realizarRetiroVisible"
    :cuenta="cuentaactual"
    @actualizar-saldo="actualizarSaldo($event)"
    @retiro-realizado="realizarRetiroVisible = false"
  />
</template>

<script>
import VerSaldo from './VerSaldo.vue';
import HacerDeposito from './HacerDeposito.vue';
import HacerRetiro from './HacerRetiro.vue';

export default {
  props: {
    cuentaactual: Object
  },
  components: {
    VerSaldo,
    HacerDeposito,
    HacerRetiro
  },
  data() {
    return {
      verSaldo: false,
      realizarDepositoVisible: false,
      realizarRetiroVisible: false
    };
  },
  methods: {
    verificarSaldo() {
      this.verSaldo = true;
    },
    realizarDeposito() {
      this.realizarDepositoVisible = true;
    },
    realizarRetiro() {
      this.realizarRetiroVisible = true;
    },
    actualizarSaldo(monto) {
      this.$emit('actualizar-saldo', monto);
    }
  }
};
</script>

<style scoped>
/* General Styles */
.menu {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 20px;
  background: #f8f9fa;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  margin: 40px auto;
}

h2 {
  color: #343a40;
  font-size: 24px;
  margin-bottom: 20px;
  font-weight: bold;
}

/* Styling for menu buttons */
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  margin: 10px 0;
}

.menu-button {
  width: 100%;
  padding: 10px 20px;
  font-size: 18px;
  font-weight: bold;
  color: white;
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.menu-button:hover {
  background-color: #0056b3;
}

.menu-button:active {
  background-color: #003d7a;
}

.menu-button:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(38, 143, 255, 0.5);
}
</style>
