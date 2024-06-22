<template>
  <div class="pokemon-container">
    <img
      v-show="revelarPokemon"
      class="imgNormal"
      :src="imagenFuente"
      alt="No se puede visualizar el Pokemon"
    />

    <img
      v-show="!revelarPokemon"
      class="img-Oscura"
      :src="imagenFuente"
      alt="No se puede visualizar el Pokemon"
    />
  </div>
</template>

<script>
export default {
  data() {
    return { mostrar: false };
  },

  props: {
    idPokemon: {
      type: Number,
      require: true,
    },
    revelarPokemon: {
      type: Boolean,
      require: true,
      default: false,
    },
  },
  computed: {
    imagenFuente() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.idPokemon}.svg`;
    },
  },
};
</script>

<style scoped>
.img-Oscura {
  filter: brightness(0);
}


.pokemon-container {
  display: flex;
  justify-content: center;
  align-items: center; 
  height: 200px;
}

img {
  height: 200px;
  width: auto;
  
}

</style>
