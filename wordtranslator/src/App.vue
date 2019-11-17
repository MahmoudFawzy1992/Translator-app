<template>
  <div id="app" class="text-center">
    <h1>Word Translator</h1>
    <h5>Powered by Vue.JS</h5>

    <translateForm v-on:formSubmit='translateText'
    />
    <translateOutput v-text="translatedText"
    />

  </div>
</template>

<script>
import translateForm from './components/translateForm'
import translateOutput from './components/translateOutput'

export default {
  name: 'App',
  components: {
    translateForm,
    translateOutput
  },
  data: function () {
    return {
      translatedText: ''
    }
  },
  methods: {
    translateText(text, language) {
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20191117T213126Z.f79359061f81d7c9.809ab73b0f1e7431657cb59a009599f94cee2b12&lang='+language+'&text='+text)
      .then((response) => {
        this.translatedText = response.body.text[0];
      })
    }
  }
}
</script>

<style>
body {
  background: #fefefe;
}

</style>
