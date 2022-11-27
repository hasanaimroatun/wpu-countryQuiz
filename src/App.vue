<template>
  <div>
    <QuizCard />
  </div>
</template>

<script>
import QuizCard from './components/QuizCards.vue'

export default {
  name: 'App',
  components: {
    QuizCard,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  content: "";
  background-image: url('assets/background.png');
  background-position: top right;
  background-repeat: no-repeat;
  background-size: 100vw;
}

@media screen and (max-width: 992px) {
  body {
    background-size: 150vw;
  }
}

@media screen and (max-width: 576px) {
  body {
    background-size: 180vw;
  }
}
</style>
