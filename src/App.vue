<template>
  <div class="app-horiz">
    <Text @giveWord='searchWord($event)'/>
    <div class="app-vert">
      <Dict :word="word" @giveDataForCard="makeCard($event)"/>
      <Card :card="card"/>
    </div>
  </div>
</template>

<script>
import Text  from '@/components/Text.vue'
import Dict  from '@/components/Dict.vue'
import Card  from '@/components/Card.vue'

export default {
  name: 'App',
  components: {
    Text, Dict, Card
  },
  data() {
    return {
      word: null,
      card: {
        word: "a",
        example: "b",
        definition: "c",
      },
    }
  },
  methods: {
    searchWord(word) {
      // console.log('jopa' + word)
      this.word = word
    },
    makeCard(card) {
      // console.log(card)
      this.card = card
    }
  }
}
</script>

<style>
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
.app-horiz {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  /* background-color: aqua; */
  margin: 0;
  padding: 0;
}
.app-vert {
  flex: 2;
  height: 100vh;
  /* background-color: blueviolet; */

  display: flex;
  flex-direction: column;

  margin: 0;
  padding: 0;
}
</style>
