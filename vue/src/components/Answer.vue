<template lang="html">
  <div class="container light-green">
    <br><br>
    <h1 class="header center lime-text text-accent-1">Congratulation!</h1>
    <div class="row center">
      <h5 class="header col s12 white-text">Your answer is correct!</h5>
    </div>
    <div class="row center">
      <a href="!#"
        class="btn-large waves-effect waves-yellow white brown-text lighten-1"
        @click.prevent="oneMore">One more?</a>
    </div>
    <br><br>
  </div>
</template>

<script>
export default {
  methods: {
    oneMore: function () {
      this.$emit('confirmed');
    },
  },
}
</script>

<style lang="css">
</style>
