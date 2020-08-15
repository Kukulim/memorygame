<template>
  <div class="container text-center">
    <div v-for="item in cards" :key="item">
      <div class="mycard" @click="selectCard(item)">
          <p v-if="lastClicked.includes(item)||discoverdCard.includes(item)">{{item}}</p>
          </div>
    </div>
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
    shuffleCards() {
      for (let i = this.cards.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.cards[i], this.cards[j]] = [this.cards[j], this.cards[i]];
      }
    },
    async selectCard(card) {
      if (this.lastClicked.length < 2) {
        this.lastClicked.push(card);
      }
      if (this.lastClicked.length == 2) {
        if (
          this.lastClicked[0].toUpperCase() == this.lastClicked[1].toUpperCase()
        ) {
          this.discoverdCard.push(this.lastClicked[0],this.lastClicked[1]);
          this.lastClicked=[];
            if(this.cards.length==this.discoverdCard.length){
                alert("brawo wygrałes");
            }
        }
        else{
            await sleep(700);
            this.lastClicked=[];
        }
      }
    },
  },
};
const sleep = m => new Promise(r => setTimeout(r, m))
</script>

<style></style>
