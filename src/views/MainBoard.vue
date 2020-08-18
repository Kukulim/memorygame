<template>
  <div class="container">
    <button class="btn btn-primary m-2 disableddiv btn-lg">DIFFICULT:</button>
    <button
      class="btn btn-primary m-2"
      @click="(difficulty = 'easy'),loadCards()"
    >
      EASY
    </button>
    <button
      class="btn btn-primary m-2"
      @click="(difficulty = 'medium'),loadCards()"
    >
      MEDIUM
    </button>
    <button
      class="btn btn-primary m-2"
      @click="(difficulty = 'hard'),loadCards()"
    >
      HARD
    </button>
    <div
      v-if="this.cards.length == this.discoverdCard.length"
      class="text-success m-5 win-info"
    >
      Congratulations you win, number of clicks: {{ timesCliked }}. To start
      again chose difficulty.
    </div>
    <div class="row mt-4">
      <div v-for="item in cards" :key="item" v-bind:class="getDifficultsize()">
        <div
          class="mycard"
          @click="selectCard(item)"
          v-bind:class="getClass(item)+ getsize()"
        >
          <img
            :src="require(`@/images/${deck}/${item.toUpperCase()}.jpg`)"
            class="img-fluid myimage"
            v-if="lastClicked.includes(item) || discoverdCard.includes(item)"
          />
        </div>
      </div>
    </div>
        <button class="btn btn-primary m-2 disableddiv btn-lg">SELECT DECK:</button>
    <button
      class="btn btn-primary m-2"
      @click="deck = 'fruit'"
    >
      FRUIT
    </button>
    <button
      class="btn btn-primary m-2"
      @click="deck = 'butterfly'"
    >
      BUTTERFLY
    </button>
        <button
      class="btn btn-primary m-2"
      @click="deck = 'flower'"
    >
      FLOWER
    </button>
  </div>
</template>

<script>
import { data } from "../shared";

export default {
  data() {
    return {
      cards: [],
      lastClicked: [],
      discoverdCard: [],
      timesCliked: 0,
      difficulty: "medium",
      deck:"fruit",
    };
  },
  created() {
    this.loadCards();
  },
  methods: {
    loadCards() {
      this.cards = [];
      switch (this.difficulty) {
        case "easy":
          this.cards = data.myCardsEasy;
          break;
        case "medium":
          this.cards = data.myCardsMedium;
          break;
        case "hard":
          this.cards = data.myCardsHard;
          break;
      }
      this.timesCliked = 0;
      this.lastClicked = [];
      this.discoverdCard = [];
      this.shuffleCards();
    },
    shuffleCards() {
      for (let i = this.cards.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.cards[i], this.cards[j]] = [this.cards[j], this.cards[i]];
      }
    },
    async selectCard(card) {
      if (this.lastClicked.length < 2) {
        this.lastClicked.push(card);
        this.timesCliked++;
      }
      if (this.lastClicked.length == 2) {
        if (
          this.lastClicked[0].toUpperCase() == this.lastClicked[1].toUpperCase() && this.lastClicked[0] != this.lastClicked[1]
        ) {
          this.discoverdCard.push(this.lastClicked[0], this.lastClicked[1]);
          this.lastClicked = [];
        } else {
          await sleep(700);
          this.lastClicked = [];
        }
      }
    },
    getClass(item) {
      if (
        this.lastClicked.includes(item) ||
        this.discoverdCard.includes(item)
      ) {
        return "disableddiv";
      }
    },
    getDifficultsize(){
      if(this.difficulty=='easy') return "col-sm-4";
      if(this.difficulty=='medium') return "col-sm-3";
      if(this.difficulty=='medium') return "col-sm-1";
    },
    getsize(){
    if(this.difficulty=="hard") return " mysmallcard";
  },
  },
};
const sleep = (m) => new Promise((r) => setTimeout(r, m));
</script>

<style></style>
