<script>
import axios from "axios";

export default {
  data() {
    return {
      cardsArray: [],
    };
  },

  methods: {
    fetchcardsArray() {
      const url = "https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0";

      axios.get(url).then((response) => {
        this.cardsArray = response.data.data;
      });
    },
  },
  mounted() {
    this.fetchcardsArray();
  },
};

</script>

<template>
  <h1 class="p-3 border-2 bg-danger mb-5">Yu-Gi-Oh</h1>
  <div class="container">
    <div class="row row-cols-5 g-5">
      <div class="col box" v-for="singleCard in cardsArray">
        <img class="cards-img" :src="singleCard.card_images[0].image_url" alt="">
        <div class="text bg-warning box-text text-center">
          <h3>{{ singleCard.name }}</h3>
          <h6>{{ singleCard.archetype }}</h6>

        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
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
