<template>
  <div id="app">
    <Breeds></Breeds>
  </div>
</template>

<script>
import Breeds from './components/Breeds'

export default {
  name: 'app',
  components: { 
    Breeds
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Noto+Sans+SC:300,400,700');
#app {
  font-family: 'Noto Sans SC', sans-serif;
  width: 1228px;
  margin: 0 auto;
}
</style>
