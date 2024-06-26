<template>
  <h1 v-if="!pokemonCorrecto">Por favor espere.........</h1>
  <div v-else>
    <h1 v-if="!mostrarFelicitaciones && !mostrarPokemonIncorrecto">
      Selecciona el Pokemon Correcto
    </h1>
    <h1 v-if="mostrarPokemonIncorrecto">
      ¡Pokemon incorrecto! Intenta de nuevo.
    </h1>
    <h1 v-if="mostrarFelicitaciones">
      Felicitaciones, seleccionaste el Pokémon correcto!
    </h1>
    <div class="puntaje">
      <h2>Intentos: {{ intentos }}</h2>
      <h2>Puntaje: {{ puntaje }}</h2>
    </div>

    <PokemonImagen :idPokemon="pokemonCorrecto.id" :revelarPokemon="mostrar" />

    <div v-if="!mostrarFelicitaciones">
      <PokemonOpciones
        :pokemons="arreglo"
        @seleccionPokemon="revisarRespuesta($event)"
      />
    </div>
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
      this.intentos++;
      if (dato.ident === this.pokemonCorrecto.id) {
        this.mostrar = true;
        this.mostrarFelicitaciones = true;
        this.mostrarPokemonIncorrecto = false;
        console.log("Pokemon Correcto...");
      } else {
        this.mostrarPokemonIncorrecto = true;
        console.log("Pokemon Incorrecto...");
      }
      this.calcularPuntaje(dato);
    },

    calcularPuntaje(dato) {
      if (dato.ident === this.pokemonCorrecto.id) {
        switch (this.intentos) {
          case 1:
            this.puntaje = 10;
            break;
          case 2:
            this.puntaje = 8;
            break;
          case 3:
            this.puntaje = 5;
            break;
          case 4:
            this.puntaje = 3;
            break;
          case 5:
            this.puntaje = 2;
            break;
          case 6:
            this.puntaje = 1;
            break;
          case 7:
            this.puntaje = 0;
            break;
          default:
            this.puntaje = 0;
        }
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
      intentos: 0,
      puntaje: 0,
    };
  },

  mounted() {
    this.cargaInicial();
  },
};
</script>

<style>
h1,
h2 {
  color: black;
}
.puntaje{
  display: flex;
  justify-content: center;
  gap: 20px;
  }
</style>
