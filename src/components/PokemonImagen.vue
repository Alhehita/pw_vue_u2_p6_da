<template>
  <div class="pokemon-container">
    <img
      v-show="mostrar"
      class="imgNormal"
      src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/54.svg"
      alt="No se puede visualizar el Pokemon"
    />

    <img
      v-show="!mostrar"
      class="img-Oscura"
      src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/54.svg"
      alt="No se puede visualizar el Pokemon"
    />
  </div>
</template>

<script>
export default {
  data() {
    return { mostrar: false };
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

.pokemon-container{
    height: 200px;
}
</style>
