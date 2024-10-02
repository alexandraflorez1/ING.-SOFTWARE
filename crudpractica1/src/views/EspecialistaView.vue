<template>
    <div id="app">
      <h1>BIENVENIDO AL SISTEMA DE ESPECIALISTA</h1>
      <label for="clave">Ingrese la clave predeterminada:  </label>
      <input
        type="password"
        v-model="clave"
        placeholder="Clave"
        id="clave"
      />
      <button @click="handleSubmit">OK</button>
      <p v-if="mensaje">{{ mensaje }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        clave: '',      // Valor ingresado por el usuario
        mensaje: '',    // Mensaje para mostrar después de presionar OK
        claveCorrecta: '1234',  // Clave predeterminada
      };
    },
    methods: {
      handleSubmit() {
        if (this.clave === this.claveCorrecta) {
          this.mensaje = 'Clave ingresada correctamente.';
        } else {
          this.mensaje = 'Clave incorrecta. Inténtalo de nuevo.';
        }
      },
    },
  };
  </script>
  
  <style>
  /* Estilos opcionales */
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  
  input {
    padding: 10px;
    font-size: 16px;
    width: 200px;
    margin-bottom: 20px;
  }
  
  button {
    padding: 10px 15px;
    font-size: 16px;
    background-color: #42b983;
    color: white;
    border: none;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #35495e;
  }
  </style>
  