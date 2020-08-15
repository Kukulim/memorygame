<template>
  <div>
    <div v-for="item in cards" :key="item">
      <div>{{ item }}</div>
    </div>
  </div>
</template>

<script>
import { data } from "../shared";

export default {
  data() {
    return {
      cards: [],
    };
  },
  created() {
    this.loadCards();
    this.shuffleCards();
  },
  methods: {
    loadCards() {
      this.cards = [];
      this.cards = data.myCards;
    },
    shuffleCards(){
            for (let i = this.cards.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.cards[i], this.cards[j]] = [this.cards[j], this.cards[i]];
    }
    }
  },
};
</script>

<style></style>