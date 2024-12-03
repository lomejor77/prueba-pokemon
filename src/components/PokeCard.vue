<template>
   <div class="pokemon-card">
      <img :src="pokemon.imageUrl" :class="{ borroso: !pokemon.discovered }" alt="Foto del Pokemon" />
      <div v-if="!pokemon.discovered" class="input-contenedor">
      <input type="text" v-model="busqueda" placeholder="¿Cuál es este Pokémon?" @keyup.enter="checkName"  />
      <button @click="checkName">Descubrir</button>
    </div>
    <p v-else>{{ pokemon.name }}</p>
   </div>
</template>
<script>
export default {
  props: {
    pokemon: {
      type: Object,
      required: true, 
    }
  },
  data() {
    return {
      busqueda: '',
    }
  },
  methods: {
    checkName() {
      if (this.busqueda.toLowerCase() === this.pokemon.name) {
        this.$emit('discover', this.pokemon.name);
      } else {
        alert('El nombre es incorrecto, vuelve a intentar');
      }
    },
  },
};
</script>
<style scoped>

.pokemon-card {
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 20px;
  text-align: center;
  align-content: center;
  margin: 10px;
  width: 200px; 
  height: 250px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.pokemon-card:hover {
  transform: scale(1.05);
}

.pokemon-card img {
  max-width: 100%;
  height: auto;
  border-radius: 5px;
}

.input-contenedor {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

.borroso {
  filter: blur(5px)  grayscale(100%);
}

input[type="text"] {
  padding: 5px; 
  margin: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 5px 10px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #218838;
}
/*.pokemon-card {
  margin: 10px;
  text-align: center;
}*/

</style>