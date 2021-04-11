<template>
  <div id="app">
    <Converter />
  </div>
</template>

<script>
import Converter from './components/Converter'

export default {
  name: "App",
  components: {
    Converter
  }
};
</script>

<style>
#app {
  width: 100vw;
  height: 100vh;

  display: flex;
  align-items: center;
  justify-content: center;

  background: var(--green-200);
}
</style>
