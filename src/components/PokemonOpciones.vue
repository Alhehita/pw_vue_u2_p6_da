<template>
  <div class="opciones-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="
          $emit('seleccionPokemon', {
            ident: pokemon.id,
            nomb: pokemon.nombre,
            test: 'Esto es una prueba',
          })
        "
      >
        {{ pokemon.nombre }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      require: true,
    },
    
  },
};
</script>

<style>
ul {
  list-style-type: none;
}

li {
  border: 1px solid rgb(131, 123, 123);
  width: 200px;
  height: 15px;
  border-radius: 5px;
  margin: 5px;
  padding: 5px;
  background: rgb(131, 123, 123);
  cursor: pointer;
  color: black;
}

li:hover {
  background: rgba(255, 255, 255, 0.5);
}

.opciones-container {
  display: flex;
  justify-content: center;
}
</style>
