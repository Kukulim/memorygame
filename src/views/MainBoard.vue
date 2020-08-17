<template>
  <div class="container">
    <div v-if="this.cards.length==this.discoverdCard.length" class="text-success m-5 win-info">Brawo wygrałeś ilość kliknięć: duzo</div>
    <div class="row mt-4">
    <div v-for="item in cards" :key="item" class="col-sm-3">
      <div class="mycard" @click="selectCard(item)" v-bind:class="getClass(item)">
          <img :src="require(`@/images/${item.toUpperCase()}.jpg`)" class="img-fluid rounded p-2" v-if="lastClicked.includes(item)||discoverdCard.includes(item)">
          </div>
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
    getClass(item){
      if(this.lastClicked.includes(item)||this.discoverdCard.includes(item)){
        return "disableddiv";
      }
    }
  },
};
const sleep = m => new Promise(r => setTimeout(r, m))
</script>

<style></style>
