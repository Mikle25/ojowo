<template>
  <div id="app">
    <Header class="header"/>
    <div class="block">
      <Navigation />
      <Main />
    </div>
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Navigation from '@/components/Navigation.vue';
import Main from '@/components/Main.vue';

export default {
  components: {
    Header, Navigation, Main,
  },
};
</script>

<style lang="scss">
$bgColor: #F0F6FC;
#app {
  max-width: 1920px;
  padding: 10px 38px 0;
  margin: 0 auto;

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: $bgColor;

}

.header {
  margin-bottom: 48px;
}

.block {
  display: grid;
  grid-template-columns: max-content 1fr;
  grid-column-gap: 163px;
}
</style>
