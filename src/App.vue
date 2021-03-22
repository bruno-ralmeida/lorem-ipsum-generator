<template>
  <div id="app">
    <h1>Lorem ipsum Generator</h1>

    <label for="paragraphs">number of paragraphs</label>
    <input
      id="paragraphs"
      type="number"
      min="1"
      v-model="numParagraphs"
      @input="generate"
    />

    <textarea id="lorem-result" v-model="lorem"  readonly></textarea>
    <div v-if="msg"><p>
      {{ msg }}</p></div>
    <button class="btn" @click="copy">copy</button>
  </div>
</template>

<script>
const LoremIpsum = require("lorem-ipsum").LoremIpsum;
export default {
  data() {
    return {
      numParagraphs: 0,
      lorem: "",
      msg: "",
    };
  },
  methods: {
    generate() {
      const lorem = new LoremIpsum({
        sentencesPerParagraph: {
          max: 8,
          min: 4
        },
        wordsPerSentence: {
          max: 16,
          min: 4
        }
      });

      if (this.numParagraphs > 0) this.lorem = lorem.generateParagraphs(parseInt(this.numParagraphs));
      else {
        this.lorem = "";
        this.msg = '';
      };

    },

    copy() {
      var copyText = document.querySelector("#lorem-result");
      copyText.select();
      var successful = document.execCommand("copy");
      this.msg = successful ? "text copied to clipboard!" : "error!";
    }
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Baloo+Da+2&display=swap");
* {
  box-sizing: border-box;
}
p,
h1,
label,
button,
#lorem-result {
  text-align: justify;
  font-family: "Baloo Da 2", cursive;
  text-transform: capitalize;
}
#paragraphs {
  padding: 0.25em 0.5em;
  border: 1px solid #efefefef;
  margin: 1em 0;
}

#paragraphs:focus {
  outline: none;
}

label,
p,
.btn,
#lorem-result {
  font-size: 16px;
}
.btn {
  padding: 0.25em 1em;
  margin: 0.5em 0;
  background: #e0e0e0;
  border: none;
}
#lorem-result {
  padding: 1em .5em;
  min-width: 80vw;
  min-height: 50vh;
  border: .5px solid #efefef;
  resize: none;
}

#lorem-result:focus {
  outline: none;
}
#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #fefefe;
}
</style>
