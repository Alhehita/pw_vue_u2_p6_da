<template>
  <div class="opciones-container">
    <ul>
      <li v-for="pokemon in pokemons" :key="pokemon.id" >{{pokemon.name}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      typeof: Array,
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
  border-radius: 5px;
  margin: 5px;
  padding: 5px;
  background: rgb(131, 123, 123);
  cursor: pointer;
}

li:hover {
  background: rgba(255, 255, 255, 0.5);
}

.opciones-container {
  display: flex;
  justify-content: center;
}
</style>
