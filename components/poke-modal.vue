<template>
  <div>
    <button
      class="button mb-3 is-link is-rounded is-outlined"
      @click="showModal()"
    >
      Learn More
    </button>

    <b-modal v-model="isModalActive" has-modal-card>
      <div class="card">
        <div class="card-content">
          <div class="content">
            <p class="title is-4 mb-1">{{ pokeInfo.name | titleize }}</p>

            <strong>Height:</strong>
            <span> {{ pokeInfo.height }} </span>
            <br />
            <strong>Weight:</strong>
            <span> {{ pokeInfo.weight }} </span>
            <br />
            <strong>Speed:</strong>
            <span v-if="pokeInfo.stats">
              {{ pokeInfo.stats[5].base_stat }}
            </span>
            <br />
            <strong>Moves:</strong>
            <span v-if="pokeInfo.moves"> {{ pokeInfo.moves.length }} </span>
            <br />
            <strong>Base XP:</strong>
            <span> {{ pokeInfo.base_experience }} </span>

            <br />
          </div>
        </div>
      </div>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: "PokeModal",
  data() {
    return { isModalActive: false };
  },
  methods: {
    showModal() {
      this.isModalActive = true;
    },
  },
  props: {
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
