<template>
  <Cutey/>
</template>

<script>
import Cutey from './components/Cutey.vue'

export default {
  name: 'App',
  components: {
    Cutey
  }
}
</script>

<style>

body {
  margin: 0;
}

#app {
  position: relative;
  
  display: grid;
  justify-items: center;
  align-items: center;

  width: 100vw;
  height: 100vh;

  overflow: hidden;

  animation: shift 80s linear infinite;
  background-size: 30px 30px;
  background-image: radial-gradient(circle, #cceeff 1px, #239e9e 1px);
}

@keyframes shift {

  0% {
    background-position: 0% 0%;
  }

  100% {
    background-position: 100% 100%;
  }

}
</style>
