<template>
  <div>
    <div class="container p-6">
      <h2 class="title is-6">POKEMON CARDS</h2>
      <h1 class="title has-text-weight-bold">Gotta catch 'em all</h1>

      <b-loading :is-full-page="isFullPage" v-model="isLoading"></b-loading>
      <div class="columns mb-5">
        <div class="column">
          <poke-card :is-loading="isLoading" :poke-info="pokeData1" />
        </div>
        <div class="column">
          <poke-card :is-loading="isLoading" :poke-info="pokeData2" />
        </div>
        <div class="column">
          <poke-card :is-loading="isLoading" :poke-info="pokeData3" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import pokeCard from "~/components/poke-card.vue";
import axios from "axios";

export default {
  components: { pokeCard },
  mounted() {
    this.fetchPokeData();
  },
  methods: {
    async fetchPokeData() {
      const pokeResult1 = await axios.get(
        "https://pokeapi.co/api/v2/pokemon/217"
      );
      const pokeResult2 = await axios.get(
        "https://pokeapi.co/api/v2/pokemon/243"
      );

      const pokeResult3 = await axios.get(
        "https://pokeapi.co/api/v2/pokemon/586"
      );

      this.pokeData1 = pokeResult1.data;
      this.pokeData2 = pokeResult2.data;
      this.pokeData3 = pokeResult3.data;
      this.isLoading = false;
    },
  },
  data() {
    return {
      isLoading: true,
      pokeData1: {},
      pokeData2: {},
      pokeData3: {},
      isFullPage: true,
    };
  },
};
</script>
