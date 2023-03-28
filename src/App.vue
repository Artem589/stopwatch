<template>
  <div class="wrapper">
    <Stopwatch />
  </div>
  
</template>
<script>
import Stopwatch from './components/Stopwatch.vue'

export default {
  components: {
    Stopwatch
  }
}
</script>
<style>

@font-face {
  font-family: "GothamPro";
  font-style: normal;
  font-weight: 400;
  src: url("@/assets/fonts/GothamProRegular.woff2") format("woff2"),
    url("@/assets/fonts/GothamProRegular.woff") format("woff");
}
  html, body {
  margin: 0px !important;
  padding: 0px !important;
  font-family: "GothamPro", sans-serif;
}
  .wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    width: 100%;
    min-height: 100vh;
    background: #353638;
    
  }
</style>
