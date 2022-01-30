<template>
  <div class="dict" @click="this.$emit('foundExpl', 'theword')">
    <div v-if="wordToShow != []">
      <WordChunk v-for="item in wordToShow" :key="item" :dictRecord="item" />
    </div>
  </div>
</template>

<script>
import WordChunk from "./WordChunk.vue";

export default {
  components: {
    WordChunk,
  },
  props: {
    word: String,
  },
  data() {
    return {
      wordToShow: [],
    };
  },
  watch: {
    word: function (newWord) {
      fetch("https://api.dictionaryapi.dev/api/v2/entries/en/" + newWord)
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          let chunks = [];

          if (data.title === "No Definitions Found") {
            this.wordToShow = [];
            return;
          }

          for (const word of data) {
            let chunk = {
              word: word["word"],
              phonetic: word["phonetic"],
              meanings: [],
            };

            for (const meaning of word["meanings"]) {
              let defs = [];
              for (const definition of meaning["definitions"]) {
                defs.push({
                  definition: definition["definition"],
                  example: definition["example"],
                });
              }

              chunk.meanings.push({
                partOfSpeech: meaning["partOfSpeech"],
                definitions: defs,
              });
            }
            chunks.push(chunk);
          }

          this.wordToShow = chunks;
        });
    },
  },
};
</script>

<style>
.dict {
  /* background-color: green; */
  flex: 4;
  overflow-y: scroll;

  border-bottom: 2px solid black;

  padding-top: 7px;
}
</style>