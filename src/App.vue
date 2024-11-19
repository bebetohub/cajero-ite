<template>
  <div>
    <h1>CAJERO ELECTRONICO ITEC</h1>
    <!--paso 3 incorporar al componente deseado-->

    <MiComponente />
    
    <VerificacionTarjeta v-if="pantalla === 'verificarTarjeta'" :cuentas="accounts" @verify-card="verifyCard" />
    <VerificarPin v-else-if="pantalla==='verificarPin'" :cuentas="accounts" :account="currentAccount" @pin-verified="pinVerified" />
    <MenuPrincipal v-else-if="pantalla==='menuPrincipal'" :cuentaactual="currentAccount" @actualizar-saldo="actualizarSaldo($event)" />
  </div>
</template>

<script>
// Paso 1: Importar los componentes
import MiComponente from './components/MiComponente.vue';
import VerificacionTarjeta from './components/VerificacionTarjeta.vue';
import VerificarPin from './components/VerificarPin.vue';
import MenuPrincipal from './components/MenuPrincipal.vue';
//import EjemploDirectiva from './components/EjemploDirectiva.vue';


// Paso 2: Exportar la respuesta que tiene para invocar al componente,
//ademas se debe definir los datos, los metodos
export default {
  name: 'App',
  components: {
    MiComponente,
    VerificacionTarjeta,
    VerificarPin,
    MenuPrincipal
    //EjemploDirectiva,
  },

  // Aquí comienza la definición de la data y otros métodos
  data() {
    return {
      accounts: [
        { cardNumber: '1234567', pin: '1234', balance: 1000 },
        { cardNumber: '8765432187654321', pin: '5678', balance: 2000 },
      ],
      currentAccount: null,
      pantalla:'verificarTarjeta',
    };
  },
  methods: {
    verifyCard(cardNumber) {
      //console.log(cardNumber +"\n" + this.accounts[0].cardNumber);
      this.currentAccount = this.accounts.find(acc => acc.cardNumber === cardNumber) || null;
      console.log(this.currentAccount);
      this.pantalla = 'verificarPin';
      //console.log(this.currentAccount + "\n");
    },
    pinVerified(){
      this.pantalla='menuPrincipal';
    },
    actualizarSaldo(monto) {
      this.currentAccount.balance += monto
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
