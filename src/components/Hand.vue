<template>
  <div class="container">
    <!-- Titre + description -->
    <h1>Jeux de carte</h1>

    <div class="row">
      <div class="col">
        <button type="button" @click="fetchAPIData">commencer</button>
      </div>
    </div>
    <div v-if="cards.length > 0" id="hand">
      <hr />
          <img v-for="card in cards" :key="card.id" :src="require('../assets/img/' + card.color +'/' + card.value + '.png')" style="margin:10px"/> 
      <hr />
    </div>
    <div class="row" v-if="cards.length > 0">
      <div class="col">
        <button type="button" @click="sortCards">trier</button>
      </div>
    </div>    
  </div>
</template>

<script>
export default {
  name: "Hand",
  data() {
    return {
      cards: [],
      responseAvailable: false,
    };
  },
  methods: {
    fetchAPIData() {
      this.responseAvailable = false;

      fetch("http://localhost:8080/api/hand", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
        },
      })
        .then((response) => {
          if (response.ok) {
            return response.json();
          } else {
            alert(
              "Server returned " + response.status + " : " + response.statusText
            );
          }
        })
        .then((response) => {
          this.cards = response.cards;
          console.log(this.cards);
          this.responseAvailable = true;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    sortCards() {
      this.responseAvailable = false;

      fetch("http://localhost:8080/api/sortedHand", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body : "{\"cards\": " + JSON.stringify(this.cards) + "}",
      })
        .then((response) => {
          if (response.ok) {
            return response.json();
          } else {
            alert(JSON.stringify(this.cards));
            alert(
              "Server returned " + response.status + " : " + response.statusText
            );
          }
        })
        .then((response) => {
          this.cards = response.cards;
          console.log(this.cards);
          this.responseAvailable = true;
        })
        .catch((err) => {
          console.log(err);
        });
    },  
},
};
</script>