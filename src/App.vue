<template>
  <div id="app">
    <h1 class="ui header inverted">新竹市消防局 勤務派遣科 新聞資訊彙整</h1>
    <small class="ui inverted header">
      version 3.1 β
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
  font-family: “微軟正黑體”;
  text-align: center;
  background: rgba(221,204,173,0.2);
}

h1.inverted, small.inverted {
  color: rgba(255,248,200,1.00) !important;
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
