<template>
  <div class="cart-miniature">
    <span>Cart {{cartItemsNumber}}</span>
  </div>
</template>

<script lang="ts">
import {Component, Prop, Vue} from 'vue-property-decorator';

@Component
export default class CartMiniature extends Vue {
  @Prop({default: 0}) cartItemsNumber!: number;
}


</script>

<style>
  .cart-miniature {
    width: 70px;
    height: 50px;
    background-color: #2c3e50;
    color: white;
    line-height: 50px;
  }
</style>
