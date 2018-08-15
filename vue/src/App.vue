<template>
  <div id="index-banner" class="parallax-container" :style="{'min-height': minHei}">
    <div class="section no-pad-bot">
      <transition name="flip" mode="out-in">
        <component
          :is="mode"
          @onAnswer="isCorrect"
          @confirmed="mode='app-questions'"></component>
      </transition>
    </div>
    <div class="parallax" :style="{'min-height': minHei}"><img :src="src" alt="Unsplashed background img 1"></div>
  </div>
</template>

<script>
import Questions from './components/Questions.vue';
import Answer from './components/Answer.vue';

export default {
  data () {
    return {
      minHei: 0,
      src: '',
      mode: 'app-questions',
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    'app-questions': Questions,
    'app-answer': Answer,
  },
  methods: {
    isCorrect: function(correct) {
      if (correct) {
        this.mode = 'app-answer';
      } else {
        alert ('Your answer is wrong!');
      }
    },
  },
  created() {
    var winhei = $(window).height();
    var navhei = $('nav').outerHeight();
    this.minHei = winhei - navhei + 'px';
    this.src = 'https://picsum.photos/1440/1200/?random';
  }
}
</script>

<style>
  .flip-enter-active {
    animation: filp-in 0.5s ease-out forwards;
  }
  .flip-leave-active {
    animation: filp-out 0.5s ease-out forwards;
  }
  @keyframes filp-out {
    from {
      transform: rotateY(0deg);
    }
    to {
      transform: rotateY(90deg);
    }
  }
  @keyframes filp-in {
    from {
      transform: rotateY(90deg);
    }
    to {
      transform: rotateY(0deg);
    }
  }
</style>
