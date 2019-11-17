<template>
  <div class="row" id="translateForm">
      <div class="col-md-6 offset-md-3 ">
            <form class="card card-body bg-light form-inline d-inline-block" v-on:submit="formSubmit">
                <input type="text" class="form-control" v-model="textToTranslate" placeholder="Enter A Word">
                <select class="form-control" v-model="language">
                    <option value="ru">Russian</option>
                    <option value="es">Spanish</option>
                    <option value="fr">French</option>
                    <option value="zh">Chinese</option>
                </select>
                <input class="btn btn-primary" type="submit" value="Translate">
            </form>
      </div>
  </div>
</template>

<script>

export default {
  name: 'translateForm',
  data() {
      return {
          textToTranslate: "",
          language: ''
      }
  },
  created() {
      this.language = 'ru';
  },
  methods: {
      formSubmit(e) {
          this.$emit('formSubmit', this.textToTranslate, this.language);
          e.preventDefault();
      }
  }
 
}
</script>

<style>
.bg-light {
    background-color: #f8f9fa!important;
}

</style>
