<template>
  <div class="text" @mouseup="showSelection()">
    <div class="uploadDiv">
      <label for="textfile" class="uploadLabel">Upload a text file to read</label>
      <input type="file" id="textfile" @change="fillTextarea" />
    </div>
    <div class="text-section">
      <pre>{{ text }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: "",
    };
  },
  methods: {
    showSelection() {
      let s = window.getSelection().toString();
      //   console.log(s)

      if (s) {
        this.$emit("giveWord", s);
      }
    },
    fillTextarea(event) {
      // console.log(event.target.files)
      let textfile = event.target.files[0];

      let reader = new FileReader();
      reader.readAsText(textfile);
      reader.onload = () => {
        // console.log(reader.result);
        this.text = reader.result;
      };
    },
  },
};
</script>

<style scoped>
.text {
  background: rgb(206, 206, 206);
  flex: 3;
  height: 100vh;
}
.text-section {
  margin: 10px;
  /* background-color: yellow; */
  background-color: white;

  height: 90%;
  overflow-y: scroll;

  padding: 5px;
  border: 1px solid black;
  border-radius: 5px;

  font-size: 1.1em;
}
.uploadDiv {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;

  height: 4%;
  padding-top: 10px;

  /* background: turquoise; */
}
label {
  /* background-color: brown; */
  font-size: 18px;
}
/* #textfile {
  background-color: aqua;
} */
pre {
  white-space: pre-wrap; /* Since CSS 2.1 */
  white-space: -moz-pre-wrap; /* Mozilla, since 1999 */
  white-space: -pre-wrap; /* Opera 4-6 */
  white-space: -o-pre-wrap; /* Opera 7 */
  word-wrap: break-word; /* Internet Explorer 5.5+ */
}
</style>