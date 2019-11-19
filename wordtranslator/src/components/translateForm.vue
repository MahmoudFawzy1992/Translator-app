<template>
  <div class="row" id="translateForm">
      <div class="col-md-6 offset-md-3 ">
            <form class="card card-body bg-light form-inline d-inline-block" v-on:submit="formSubmit">
                <input type="text" class="form-control" v-model="textToTranslate" placeholder="Enter A Word">
                <select class="form-control" v-model="language">
                    <option v-for="(langeName, langCode) in langSelect" :key="langeName" :value="langCode">{{langeName}}</option>
                </select>
                <input class="btn btn-primary" :disabled="textToTranslate == isDisabled" type="submit" value="Translate">
            </form>
      </div>
  </div>
</template>

<script>

export default {
  name: 'translateForm',
  data() {
      return {
          textToTranslate: '',
          language: '',
          isDisabled: null,
          langSelect: {}
      }
  },
  mounted() {
      this.isDisabled = this.textToTranslate;
      
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/getLangs?key=trnsl.1.1.20191117T213126Z.f79359061f81d7c9.809ab73b0f1e7431657cb59a009599f94cee2b12&ui=langs')
      .then((response) => {
        this.langSelect = response.body.langs
        // console.log(response.body.langs);
      });
  },
  methods: {
      formSubmit(e) {
          this.$emit('formSubmit', this.textToTranslate, this.language, this.langSelect);
          e.preventDefault();
      },
      
  }
 
}
</script>

<style>
.bg-light {
    background-color: #f8f9fa!important;
}

</style>
