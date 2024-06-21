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
      typeof: Number,
      require: true,
    },
    revelarPokemon: {
      typeof: Boolean,
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

img {
  height: 200px;
  width: auto;
  position: absolute;
  right: 45%;
}

.pokemon-container {
  height: 200px;
}
</style>
