<template>
  <div class="card" v-if="card">
    <textarea cols="50" rows="3" v-model="top"></textarea>
    <textarea cols="50" rows="3" v-model="bottom"></textarea>
    <div class="btns">
      <div class="status">
        Cards saved: {{ cards.length }}
      </div>
      <button @click="saveCard">Save the card</button>
      <button @click="downloadCSV">Download .csv</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["card"],
  data() {
    return {
      top: "",
      bottom: "",
      cards: [],
    };
  },
  // computed: {
  //   cardsAmount: () => {
  //     return this.cards.length;
  //   }
  // },
  watch: {
    card: function (newCard) {
      console.log("From card component");
      // console.log(newCard);

      this.top = newCard.example;
      this.bottom = newCard.word + " - " + newCard.definition;
    },
  },
  methods: {
    saveCard() {
      if (this.top === "" && this.bottom === "") return;
      if (!this.example) {
        this.example = this.definition;
      }
      this.cards.push({
        example: this.top,
        definition: this.bottom,
      });
    },
    downloadCSV() {
      let csv = "Example, Definition\n";

      for (const exercise of this.cards) {
        csv += exercise.example + "," + exercise.definition + "\n";
      }

      let hiddenElement = document.createElement("a");
      hiddenElement.href = "data:text/csv;charset=utf-8," + encodeURI(csv);
      hiddenElement.target = "_blank";

      //provide the name for the CSV file to be downloaded
      hiddenElement.download = "cards.csv";
      hiddenElement.click();
    },
  },
};
</script>

<style scoped>
.card {
  /* background: blue; */
  flex: 2;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.card-input {
  width: 80%;
  height: 30%;
}
.btns {
  display: flex;
  flex-direction: row;
}
.status {
  margin-top: 2px;
}
button {
  display: block;
  margin-left: 10px;
  margin-right: 15px;
}
</style>