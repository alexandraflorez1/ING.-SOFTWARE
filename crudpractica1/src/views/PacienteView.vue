<template>
  <div id="app">
    <h1>Búsqueda de resultados</h1>
    <label for="documento">Ingrese el número de documento:  </label>
    <input
      type="text"
      v-model="documento"
      placeholder="Número de documento"
      id="documento"
    />
    <button @click="handleSubmit">OK</button>
    <p v-if="mensaje">{{ mensaje }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      documento: '', // Valor inicial del número de documento
      mensaje: '',    // Mensaje para mostrar después de presionar OK
    };
  },
  methods: {
    handleSubmit() {
      if (this.documento) {
        this.mensaje = `Número de documento ${this.documento} ingresado correctamente.`;
      } else {
        this.mensaje = 'Por favor, ingrese un número de documento.';
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
