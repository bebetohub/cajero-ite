<template>
  <div id="app">
    <div class="header">
      <h1>💳 Cajero Electrónico ITEC</h1>
    </div>

    <!-- Renderizado dinámico de componentes según la pantalla -->
    <div class="content">
      <VerificacionTarjeta v-if="pantalla === 'verificarTarjeta'" :cuentas="accounts" @verify-card="verifyCard" />
      <VerificarPin v-else-if="pantalla === 'verificarPin'" :cuentas="accounts" :account="currentAccount"
        @pin-verified="pinVerified" />
      <MenuPrincipal v-else-if="pantalla === 'menuPrincipal'" :cuentaactual="currentAccount"
        @actualizar-saldo="actualizarSaldo" />
    </div>
  </div>
</template>

<script>
import VerificacionTarjeta from './components/VerificacionTarjeta.vue';
import VerificarPin from './components/VerificarPin.vue';
import MenuPrincipal from './components/MenuPrincipal.vue';

export default {
  name: 'App',
  components: {
    VerificacionTarjeta,
    VerificarPin,
    MenuPrincipal
  },
  data() {
    return {
      accounts: [
        { cardNumber: '4111111111111111', pin: '1234', balance: 1000 },
        { cardNumber: '5500000000000004', pin: '5678', balance: 2000 },
      ],
      currentAccount: null,
      pantalla: 'verificarTarjeta'
    };
  },
  methods: {
    verifyCard(cardNumber) {
      this.currentAccount =
        this.accounts.find((acc) => acc.cardNumber === cardNumber) || null;
      if (this.currentAccount) {
        this.pantalla = 'verificarPin';
      }
    },
    pinVerified() {
      this.pantalla = 'menuPrincipal';
    },
    actualizarSaldo(monto) {
      if (this.currentAccount) {
        this.currentAccount.balance += monto;
      }
    }
  }
};
</script>

<style scoped>
/* Estilo general */
#app {
  font-family: 'Arial', sans-serif;
  color: #2c3e50;
  background-color: #f4f4f9;
  text-align: center;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0;
}

/* Encabezado */
.header {
  background-color: #007bff;
  color: #fff;
  padding: 20px;
  width: 100%;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.header h1 {
  font-size: 2rem;
  margin: 0;
  font-weight: 600;
}

/* Contenido principal */
.content {
  background: #ffffff;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  width: 90%;
  max-width: 500px;
  margin-top: 20px;
}
</style>
