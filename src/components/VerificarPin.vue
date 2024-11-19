<template>
  <div>
    <h1>VERIFICAR PIN</h1>
    <input type="password" v-model="pin_local" placeholder="INTRODUCIR PIN"><br><br>
    <button @click="verifyPin"> Verificar PIN</button>
    <p v-if="errorMessage">{{ errorMessage }}</p>
    <MenuPrincipal v-if="pinCorrecto" :cuenta="account"/>
  </div>
</template>

<script>
import MenuPrincipal from './MenuPrincipal.vue';

export default{
    props:{
      cuentas:Array,
      account: Object
  },
  components:{
    MenuPrincipal,
  },
  data(){
    return{
      pin_local:"",
      errorMessage:"",
      pinCorrecto:false
    };
  },
  methods:{
    verifyPin(){
      const cuenta = this.cuentas.find((acc)=>acc.cardNumber === this.account.cardNumber);
      if(cuenta && cuenta.pin === this.pin_local)
      {
        this.errorMessage="PIN ENCONTRADO";
        this.$emit('pin-verified');
        this.pinCorrecto = true;
      }
      else
      {
        this.errorMessage = "PIN INCORRECTO";
      }
    },
  },
};
</script>

