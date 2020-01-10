<template>
  <div class="product-page__container">
    <div class="product-page__leftcol">
      Products image
    </div>
    <div class="product-page__rightcol">
      <h1>{{title}}</h1>
      <span>Shipping: 1 day</span>
      <span>Stock: {{isOnStock ? "available" : "out of stock"}}</span>
      <h3>{{message}}</h3>
      <h2>Details</h2>
      <ul v-for="detail in details" v-bind:key="detail">
        <li>{{detail}}</li>
      </ul>
      <h2>Colors:</h2>
      <ul v-for="color in colors" v-bind:key="color">
        <li>{{color}}</li>
      </ul>
      <button v-on:click="addToCart">Add to Cart</button>
    </div>
  </div>
</template>

<script lang="ts">
  // import {Component, Prop, Vue} from 'vue-property-decorator';
  import Vue, {ComponentOptions} from 'vue';

  interface ProductPage extends Vue {
    title: string;
    message: string;
    isOnStock: boolean;
    onClick (): void;
    details: string[];
    colors: string[];
  }

  export default {
    data: function () {
      return {
        title: "Vue Mastery Socks",
        message: "Welcome to products page",
        isOnStock: true,
        details: ["80% cotton", "20% polyester", "gender neutral"],
        colors: ["Green", "Blue"]
      }
    },
    methods: {
      addToCart: function () {
        console.log(this.message + ' ' + this.colors[0])
      }
    }
  } as ComponentOptions<ProductPage>

</script>

<style lang="scss" scoped>

.product-page__container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.product-page__rightcol {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

</style>
