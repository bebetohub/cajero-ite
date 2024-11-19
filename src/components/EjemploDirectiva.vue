<template>
  <div>
    <br><br>
    {{ Super_usuario }}
    <br><br>
    Super Usuario:<input v-model="Super_usuario" placeholder="el es el super usuario"><br><br>
  </div>
  <div>
    <p v-if="estaLogueado">Bienvenido {{ usuario }} {{ contraseña }}</p>
    <p v-else>Iniciar sesion</p>

    <div v-if="estaLogueado">
      Usuario:<input v-model="usuario" placeholder="Ingresa tu usuario"><br><br>
      Contraseña:<input v-model="contraseña" placeholder="Ingrese su contraseña">
    </div>
    <button @click="cambioValor">{{ estaLogueado ? 'Cerrar sesión' : 'Iniciar sesión' }}</button>
  </div>
  <div v-if="estaLogueado">
    <h3>LISTA DE USUARIOS</h3>
    <ul>
      <li v-for="(user,index) in usuarios" :key="index"> {{ user }}     </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return { estaLogueado: false, usuario:"",contraseña:"",Super_usuario:"Administrador", usuarios:['Carlos','Ana','Luis'], };
  },
  methods: {
    cambioValor() {
      this.estaLogueado = !this.estaLogueado;
    },
  },
};
</script>