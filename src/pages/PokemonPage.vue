<template>
  <h1 v-if="!pokemonCorrecto">Por favor espere.........</h1>
  <div v-else>
    <h1 v-if="!mostrarFelicitaciones && !mostrarPokemonIncorrecto">
      Selecciona el Pokemon Correcto
    </h1>

    <PokemonImagen :idPokemon="pokemonCorrecto.id" :revelarPokemon="mostrar" />

    <div v-if="!mostrarFelicitaciones">
      <PokemonOpciones
        :pokemons="arreglo"
        @seleccionPokemon="revisarRespuesta($event)"
      />
    </div>

    <h1 v-if="mostrarFelicitaciones">
      Felicitaciones, seleccionaste el Pokémon correcto!
    </h1>
    <h1 v-if="mostrarPokemonIncorrecto">
      ¡Pokemon incorrecto! Intenta de nuevo.
    </h1>
  </div>
</template>

<script>
import PokemonImagen from "@/components/PokemonImagen.vue";
import PokemonOpciones from "@/components/PokemonOpciones.vue";

import obtenerPokemonsFachada from "../clientes/ClientePokemonAPI.js";

export default {
  components: {
    PokemonImagen,
    PokemonOpciones,
  },

  methods: {
    async cargaInicial() {
      const vectorInicial = await obtenerPokemonsFachada(7);
      this.arreglo = vectorInicial;

      const inidice = Math.floor(Math.random() * 7);

      this.pokemonCorrecto = this.arreglo[inidice];
    },
    revisarRespuesta(dato) {
      console.log("Se emitió un evento desde el hijo");
      console.log(dato);
      if (dato.ident === this.pokemonCorrecto.id) {
        this.mostrar = true;
        this.mostrarFelicitaciones = true;
        this.mostrarPokemonIncorrecto = false;
        console.log("Pokemon Correcto...");
      } else {
        this.mostrarPokemonIncorrecto = true;
        console.log("Pokemon Incorrecto...");
      }
    },
  },
  data() {
    return {
      arreglo: [],
      pokemonCorrecto: null,
      mostrar: false,
      mostrarFelicitaciones: false,
      mostrarPokemonIncorrecto: false,
    };
  },

  mounted() {
    this.cargaInicial();
  },
};
</script>

<style></style>
