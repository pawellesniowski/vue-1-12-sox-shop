<template>
  <div id="app">
    <CartMiniature :cartItemsNumber="cartItems.length"/>
    <ProductPage @add-to-cart="addToCart" @remove-from-cart="removeFromCart"/>
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
  cartItems: number[] = [];
  addToCart (id: number): void {
    this.cartItems.push(id);
  }
  removeFromCart (id: number) {
    const indexIdToRemove = this.cartItems.indexOf(id);
    this.cartItems = this.cartItems.filter((item, index) => index !== indexIdToRemove);
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
