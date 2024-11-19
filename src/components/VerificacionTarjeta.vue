<template>
 <div>
    <h2>Verificación de Tarjeta</h2>
    <input type="text" v-model="cardNumber" placeholder="Número de tarjeta" /><br><br>
    <button @click="verifyCard">Verificar</button>
    <p v-if="errorMessage">{{ errorMessage }}</p>
    <VerificarPin v-if="cardfound" :cuentas="cuentas" :account="currentaccount" @pin-verified="pinVerified"/>
  
 </div>
</template>

<script>
import VerificarPin from './VerificarPin.vue';
export default {
  //DEFINIMOS LA PROPIEDADES PARA EL COMPONENTE
  props:{
    cuentas:Array,
  },
  components:{
    VerificarPin,
  },
  data() {
    return {
      cardNumber: '',
      errorMessage: '',
      cardfound:false,
      verificacionPin:'',
      currentaccount:null,
    };
  },
  methods: {
    verifyCard() {
      this.currentaccount = this.cuentas.find((acc)=>acc.cardNumber === this.cardNumber);
      if (!this.currentaccount) {
        this.errorMessage = 'Tarjeta no encontrada';
      } else {
        this.$emit('verify-card',this.cardNumber);
        this.errorMessage = 'Su numero es correcto';
        this.verificacionPin = true;
        this.cardfound = true;
        //console.log(this.currentaccount);
      }
    },
    verifyPin(){
      console.log('Pin Verficado');
    },
  },
};
</script>

<style>

</style>