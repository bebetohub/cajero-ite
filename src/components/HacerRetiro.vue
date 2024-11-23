<template>
    <div>
        <h2>Realizar Retiro</h2>
        <form @submit.prevent="realizarRetiro">
            <label for="monto-retiro">Monto:</label>
            <input id="monto-retiro" type="number" v-model.number="monto" placeholder="Ingresa el monto a retirar"
                min="1" required />
            <button type="submit">Retirar</button>
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
        realizarRetiro() {
            if (this.monto <= 0) {
                alert("El monto debe ser mayor a 0.");
                return;
            }

            if (this.monto > this.cuenta.saldo) {
                alert("Fondos insuficientes. No puedes retirar más de lo disponible.");
                return;
            }

            // Emite el evento para actualizar el saldo
            this.$emit('actualizar-saldo', -this.monto);

            // Emite el evento para notificar que se realizó el retiro
            this.$emit('retiro-realizado');

            // Resetea el campo de monto
            this.monto = 0;

            alert("Retiro realizado con éxito.");
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
    background-color: #dc3545;
    color: #fff;
    border: none;
    padding: 10px;
    cursor: pointer;
}

button:hover {
    background-color: #a71d2a;
}
</style>