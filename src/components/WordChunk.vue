<template>
  <div class="base">
    <div class="top">
      <div class="wordWriting">{{ dictRecord.word }}</div>
      <div class="wordSpelling">{{ dictRecord.phonetic }}</div>
    </div>
    <div class="explanation" v-for="part in dictRecord.meanings" :key="part">
      <div class="partOfSpeech">
        <p>
        {{ part.partOfSpeech }}
        </p>
      </div>
      <div class="usage">
        <div
          class="exampleExplanation"
          v-for="definition in part.definitions"
          :key="definition"
        >
          <div class="exampleWrapper">
            <div class="definition">{{ definition.definition }}</div>
            <div class="example">{{ definition.example }}</div>
          </div>
          <div
            class="btnMakeCard"
            @click="
              saveWord(
                dictRecord.word,
                definition.example,
                definition.definition
              )
            "
          >
            <button>+</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["dictRecord"],
  methods: {
    saveWord(word, example, definition) {
      let card = {
        word,
        example,
        definition,
      };
      this.$parent.$emit("giveDataForCard", card);
    },
  },
};
</script>

<style scoped>
.base {
  display: flex;
  flex-direction: column;
}
.top {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  /* background-color: yellow; */   
  width: 80%;
  align-self: center;
  background-color: rgb(141, 143, 255);
}
.wordWriting {
    font-weight: bold;
}
.explanation {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  /* background-color: violet; */
  margin: 5px 0;
}
.partOfSpeech {
  flex: 1;
  align-self: center;
  /* background-color: red; */
  text-align: center;
  /* height: 90%; */
  margin: 0 5px;
}
.usage {
  flex: 7;
  display: flex;
  flex-direction: column;
  margin: 5px 0;

  border-left: 2px dotted grey;
}
.exampleExplanation {
  /* background-color: salmon; */
  margin: 5px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 2px 5px;
}
.exampleWrapper {
  display: flex;
  flex-direction: column;

  border: 1px solid grey;
  border-radius: 5px;
  padding: 3px;
}
.definition {
    border-bottom: 1px dashed black;
}
.example {
    padding-top: 3px;
    font-style: italic;
}
</style>    