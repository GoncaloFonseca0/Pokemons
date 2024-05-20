<template>
  
  <div id="app">
    <h1>Welcome Pokemon lover's!</h1>

    <div class="container">
      <h2>Pick a random Pokemon!</h2>
      <div class="card">
        <div class="pokemon-info" v-if="pokemon">
          <img :src="pokemon.sprites.front_default" alt="pokemon image">
          <p>Name: {{ pokemon.name }}</p>
          <p>HP: {{ pokemon.stats[0].base_stat }}</p>
          <p>Type: {{ pokemon.types[0].type.name }}</p>
        </div>
      </div>
      <button class="switch-button" @click="fetchPokemon('pokemon')">Switch Pokemon</button>
    </div>
  </div>


  <div class="battle">
  <h1 >
    Join the Arena! 
  </h1>
<div class="battle_one">
    <div class="container">
      <h2>Player One</h2>
      <div class="card">
        <div class="pokemon-info" v-if="pokemonOne">
          <img :src="pokemonOne.sprites.front_default" alt="pokemon image">
          <p>Name: {{ pokemonOne.name }}</p>
          <p>HP: {{ pokemonOne.stats[0].base_stat }}</p>
          <p>Type: {{ pokemonOne.types[0].type.name }}</p>
        </div>
      </div>
      <button class="switch-button" @click="fetchPokemon('pokemonOne')">Switch Pokemon</button>
    </div>
    <button class="button" @click="fight" >Fight!</button>

    <div class="container">
      <h2>Player Two</h2>
      <div class="card">
        <div class="pokemon-info" v-if="pokemonTwo">
          <img :src="pokemonTwo.sprites.front_default" alt="pokemon image">
          <p>Name: {{ pokemonTwo.name }}</p>
          <p>HP: {{ pokemonTwo.stats[0].base_stat }}</p>
          <p>Type: {{ pokemonTwo.types[0].type.name }}</p>
        </div>
      </div>
      <button class="switch-button" @click="fetchPokemon('pokemonTwo')">Switch Pokemon</button>
    </div>

  </div>
  </div>


</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      pokemon:null,
      pokemonOne: null,
      pokemonTwo: null,
    };
  },
  methods: {
    fetchPokemon(player) {
      const pokemonId = Math.floor(Math.random() * 200) + 1;  // Random pokemons
      axios.get(`https://pokeapi.co/api/v2/pokemon/${pokemonId}`)
        .then(response => {
          this[player] = response.data;
        });
    },
    fight() {
      // the Pokemon with higher base HP wins
      if (this.pokemonOne.stats[0].base_stat > this.pokemonTwo.stats[0].base_stat) {
        alert(`${this.pokemonOne.name} wins!`);
        this.fetchPokemon(this.pokemonOne);
        
      } else if (this.pokemonOne.stats[0].base_stat < this.pokemonTwo.stats[0].base_stat) {
        
        alert(`${this.pokemonTwo.name} wins!`);
      } else {
        alert('It\'s a draw!');
      }
    },
  },
  created() {
    this.fetchPokemon('pokemon'); // default pokemon
    this.fetchPokemon('pokemonOne');// default pokemon
    this.fetchPokemon('pokemonTwo');// default pokemon
  },
};
</script>

<style scoped>

header{
  padding: 5em;
}
  body, html {
  
  width: 100%;
  height: 100%;
  font-family: Arial, sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f0f8ff; 
}



#app {
  padding:5em;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom right, #a1c4fd, #c2e9fb);
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 50px;
  width: 100%;
  max-width: 500px;
  background-color: #fff;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  border-radius: 10px;
}

h1 {
  padding: 1em;
  color: #333;
  font-size: 50px;
  display: flex;
  flex-direction: column;
  text-align: center;
}
h2 {
  color: #333;
  font-size: 30px;
  padding: 0em;
}

.pokemon-info {
  margin-bottom: 20px;
  text-align: center;
}

.pokemon-info img {
  width: 150px;
  height: 150px;
}

.pokemon-info p {
  margin: 5px 0;
  color: #555;
}

.switch-button {
  margin-top: 10px;
  padding: 10px 20px;
  background-color: #f8d030;
  border: none;
  border-radius: 5px;
  color: #3d7dca;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.switch-button:hover {
  background-color: #f8bf30;
}



.button{

  padding: 20px;
  margin: 20px;
  background-color: #f8d030;
  border: none;
  border-radius: 5px;
  color: #3d7dca;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  
}

.battle{
  background: linear-gradient(to bottom right, #a1c4fd, #c2e9fb);
  padding-bottom:2em;
  
}
.battle_one{
  display: flex;
  flex-direction: row;
}

</style>