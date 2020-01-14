<template>
  <div id="app">
    <CartMiniature :cartItemsNumber="cartItemsNumber"/>
    <ProductPage :handleItemsToCart="handleItemsToCart"/>
    <AppFooter/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import ProductPage from './views/ProductPage.vue';
import AppFooter from './components/AppFooter.vue';
import CartMiniature from './components/CartMiniature.vue';

@Component({
  components: {
    ProductPage,
    AppFooter,
    CartMiniature,
  },
})
export default class App extends Vue {
  cartItemsNumber: number = 0;
  handleItemsToCart () {
    this.cartItemsNumber++;
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
