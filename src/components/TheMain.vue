<script>
import axios from "axios";

export default {
  data() {
    return {
      cardsArray: [],
      archetype: [],
      selectedArchetype: null,
    };
  },

  methods: {
    fetchcardsArray() {
      const url = "https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0";

      axios.get(url).then((response) => {
        this.cardsArray = response.data.data;
      });
    },

    fetchcardsArchetype() {
      const url = "https://db.ygoprodeck.com/api/v7/archetypes.php";

      axios.get(url).then((response) => {
        this.archetype = response.data;
        console.log(this.archetype)
      });
    },

  },

  computed: {
  filteredCards() {
    if (!this.selectedArchetype) {
      return this.cardsArray;
    }
    
    return this.cardsArray.filter(card => card.archetype === this.selectedArchetype);
  },
},

  mounted() {
    this.fetchcardsArray();
    this.fetchcardsArchetype();
  },
};

</script>

<template>
  <h1 class="p-3 border-2 bg-danger mb-5">Yu-Gi-Oh</h1>
  <div class="container">
    <div class="row row-cols-5 g-5">
      <select class="form-select" v-model="selectedArchetype" aria-label="Default select example">
        <option value="" selected>Seleziona Archetipo</option>
        <option v-for="singleArchetype in archetype" :value="singleArchetype.archetype_name">{{singleArchetype.archetype_name}}</option>
      </select>
      <div class="col box" v-for="singleCard in filteredCards">
        <img class="cards-img" :src="singleCard.card_images[0].image_url" alt="">
        <div class="text bg-warning box-text text-center">
          <h3>{{ singleCard.name }}</h3>
          <h6>{{ singleCard.archetype }}</h6>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.box {
  max-height: 600px;

  .cards-img {
    width: 100%;
  }

  .box-text {
    min-height: 180px;
  }
}
</style>
