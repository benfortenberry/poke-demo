

<template>
  <div class="card">
    <div class="card-image">
      <figure class="image is-4by3 gray-background" >
        <img v-if="!isLoading"
          :src="pokeInfo.sprites.other.dream_world.front_default"
        />
      </figure>
    </div>
    <div class="card-content">
      <div class="content">
        <b-skeleton v-if="isLoading" :animated="isAnimated"></b-skeleton>

        <b-skeleton v-if="isLoading" width="50%" :animated="isAnimated"></b-skeleton>

        <b-skeleton v-if="isLoading"  width="10%" :animated="isAnimated"></b-skeleton>


        <p class="title is-4 mb-2">{{ pokeInfo.name | titleize }}</p>
        <p v-if=!isLoading>
          <strong>Abilities:</strong>
          <span v-for="(ability, a) in pokeInfo.abilities" :key="'a'+a"
            >{{ ability.ability.name  | titleize }}<span v-if="pokeInfo.abilities.length > (a + 1)">, </span
            >
              </span
          >
         
          <br />
          <strong>Type:</strong>
          <span v-for="(type, i) in pokeInfo.types" :key="i">
           {{ type.type.name | titleize }}<span v-if="pokeInfo.types.length > (i + 1)">, </span
            >
          </span>

          <br />
          <section v-if="pokeInfo.stats">
                 <strong>HP:</strong> {{ pokeInfo.stats[0].base_stat }} <br />
          <strong>Attack:</strong> {{ pokeInfo.stats[1].base_stat }}<br />
          <strong>Defense:</strong> {{ pokeInfo.stats[2].base_stat }}
          </section>
       
        </p>

        <poke-modal   v-if="!isLoading" :poke-info="pokeInfo" :active="isModalActive" />

      </div>
    </div>
  </div>
</template>


<script>
import pokeModal from "./poke-modal.vue";
export default {
  components: { pokeModal },
  name: "PokeCard",
  data() {
    return {
      isAnimated: true,
      isModalActive: false,
    };
  },
  props: {
    isLoading: {
      type: Boolean,
      default: function () {
        return true;
      },
    },
    pokeInfo: {
      type: Object,
      default: function () {
        return {};
      },
    },
  },
  filters: {
    titleize(value) {
      if (value) {
        return value.replace(/(?:^|\s|-)\S/g, (x) => x.toUpperCase());
      }
    },
  },
};
</script>
