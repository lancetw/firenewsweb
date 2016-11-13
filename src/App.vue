<template>
  <div id="app">
    <h1 class="ui header inverted">新竹市消防局 勤務派遣科 新聞資訊彙整</h1>
    <small class="ui inverted header">
      version 5.1
    </small>
    <news></news>
  </div>
</template>

<script>
import '../semantic/dist/semantic.js'
import News from './components/News'

export default {
  components: {
    News
  }
}
</script>

<style lang="scss">
@import "../semantic/dist/semantic.css";

html {

}

body {
  font-family: "微軟正黑體";
  text-align: center;
  background: rgba(190,180,150,0.1);
  background:
    linear-gradient(
      rgba(0, 0, 0, 0.01),
      rgba(0, 0, 0, 0.5)
    ),
    url(https://source.unsplash.com/collection/183254/urban-essentials);
  background-size: cover;
  background-attachment: fixed;
}

h1.ui.inverted, small.ui.inverted {
  font-family: "微軟正黑體" !important;
  color: rgba(251,251,251,1) !important;
  text-shadow: 0 0 2px #333;
}

#app {
  margin: 0 auto;
  color: #2c3e50;
  max-width: 960px;
  text-align: center;
  padding: 20px 40px;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px;
}

</style>
