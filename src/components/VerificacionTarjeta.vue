<template>
  <div class="verification-container">
    <h2>🔒 Verificación de Tarjeta</h2>
    <div class="form-group">
      <div class="input-container">
        <input type="text" v-model="formattedCardNumber" @input="formatCardNumber" maxlength="19"
          placeholder="Ejemplo: 4111 1111 1111 1111" class="input-field" />
        <span class="input-icon">💳</span>
      </div>
      <button class="verify-button" @click="verifyCard">Verificar</button>
    </div>
    <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
    <VerificarPin v-if="cardfound" :cuentas="cuentas" :account="currentaccount" @pin-verified="pinVerified" />
  </div>
</template>

<script>
import VerificarPin from './VerificarPin.vue';
export default {
  props: {
    cuentas: Array
  },
  components: {
    VerificarPin
  },
  data() {
    return {
      cardNumber: '',
      formattedCardNumber: '',
      errorMessage: '',
      cardfound: false,
      verificacionPin: '',
      currentaccount: null
    };
  },
  methods: {
    formatCardNumber() {
      // Elimina caracteres no numéricos
      this.cardNumber = this.formattedCardNumber.replace(/\D/g, '');
      // Divide en bloques de 4 dígitos
      this.formattedCardNumber = this.cardNumber
        .replace(/(\d{4})(?=\d)/g, '$1 ')
        .trim();
    },
    verifyCard() {
      if (this.cardNumber.length !== 16) {
        this.errorMessage = '❌ El número de tarjeta debe tener 16 dígitos';
        return;
      }

      this.currentaccount = this.cuentas.find(
        (acc) => acc.cardNumber === this.cardNumber
      );
      if (!this.currentaccount) {
        this.errorMessage = '❌ Tarjeta no encontrada';
      } else {
        this.$emit('verify-card', this.cardNumber);
        this.errorMessage = '✅ Número de tarjeta correcto';
        this.verificacionPin = true;
        this.cardfound = true;
      }
    }
  }
};
</script>

<style scoped>
.verification-container {
  max-width: 400px;
  margin: 40px auto;
  padding: 20px;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
  font-family: 'Arial', sans-serif;
}

h2 {
  color: #333333;
  font-size: 24px;
  margin-bottom: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.input-container {
  position: relative;
  width: 100%;
}

.input-field {
  width: 100%;
  padding: 10px 15px;
  font-size: 16px;
  border: 1px solid #cccccc;
  border-radius: 6px;
  margin-bottom: 15px;
  box-sizing: border-box;
  transition: border-color 0.3s ease;
}

.input-field:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 4px rgba(0, 123, 255, 0.3);
}

.input-icon {
  position: absolute;
  top: 50%;
  right: 15px;
  transform: translateY(-50%);
  font-size: 20px;
  color: #666666;
}

.verify-button {
  padding: 10px 20px;
  font-size: 16px;
  font-weight: bold;
  color: #ffffff;
  background-color: #007bff;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.verify-button:hover {
  background-color: #0056b3;
}

.verify-button:active {
  background-color: #003d7a;
}

.error-message {
  color: #d9534f;
  font-size: 14px;
  margin-top: 10px;
  font-weight: bold;
}
</style>
