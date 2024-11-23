<template>
  <div>
    <h2>Realizar Depósito</h2>
    <form @submit.prevent="realizarDeposito">
      <label for="monto">Monto:</label>
      <input 
        id="monto" 
        type="number" 
        v-model.number="monto" 
        placeholder="Ingresa el monto"
        min="1" 
        required 
      />
      <button type="submit">Depositar</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    cuenta: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      monto: 0
    };
  },
  methods: {
    realizarDeposito() {
      if (this.monto <= 0) {
        alert("El monto debe ser mayor a 0.");
        return;
      }

      // Emite el evento para actualizar el saldo
      this.$emit('actualizar-saldo', this.monto);

      // Emite el evento para notificar que se realizó el depósito
      this.$emit('deposito-realizado');

      // Resetea el campo de monto
      this.monto = 0;

      alert("Depósito realizado con éxito.");
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-width: 300px;
}

button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 10px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>