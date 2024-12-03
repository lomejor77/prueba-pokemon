<template>
    <div class="container">
        <div>
            <h2>Pokémones descubiertos: {{ counter }}</h2>
        </div>
        <div class="grid">
            <PokeCard v-for="pokemon in pokemones" :key="pokemon.name" :pokemon="pokemon" @discover="handleDiscover" />
        </div>
    </div>

</template>
<script>

import axios from 'axios';
import PokeCard from './PokeCard.vue';


export default {
    components: {
        PokeCard
    },
    data() {
        return {
            pokemones: [],
            counter: 0,
        };
    },

    mounted() {
        this.fetchPokemones();
    },
    methods: {
        async fetchPokemones() {
            try {
                const url = "https://pokeapi.co/api/v2/pokemon?limit=20";
                const response = await axios.get(url);
                const promises = response.data.results.map(async (pokemon) => {
                    const detailResponse = await axios.get(pokemon.url);
                    return {
                        name: pokemon.name,
                        imageUrl: detailResponse.data.sprites.front_default,
                        discovered: false,
                    };
                });
                this.pokemones = await Promise.all(promises);
            } catch (error) {
                console.log("Error: no se pueden cargar los pokémones", error);
            }
        },
        handleDiscover(pokemonName) {
            const pokemon = this.pokemones.find(p => p.name === pokemonName);
            if (pokemon && !pokemon.discovered) {
                pokemon.discovered = true;
                this.counter += 1;
            }
        },
    }
};
</script>
<style scope>
.grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: auto;
    gap: 16px;
    padding: 10px;
}
</style>