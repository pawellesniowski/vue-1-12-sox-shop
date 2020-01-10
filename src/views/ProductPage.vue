<template>
  <div class="product-page__container">
    <div class="product-page__leftcol">
      {{soxColor}}
      <img :src="soxImage">
    </div>
    <div class="product-page__rightcol">
      <h1>{{title}}</h1>
      <span>Shipping: 24 hours</span>
      <span>Stock: {{inventory > 0 ? "available" : "out of stock"}}</span>
      <h2>Details</h2>
      <ul v-for="detail in details" v-bind:key="detail.id">
        <li>{{detail.material}}</li>
      </ul>
      <h2>Colors:</h2>
      <ul v-for="color in colors" v-bind:key="color">
        <li v-on:click="setSoxColor(color)">{{color}}</li>
      </ul>
      <button v-on:click="handleAddToCart">Add to Cart</button>
    </div>
  </div>
</template>

<script lang="ts">
  import {Component, Prop, Vue} from 'vue-property-decorator';

  interface materialDetails {
    id: number;
    material: string;
  }

  @Component
  export default class ProductPage extends Vue {
    @Prop() handleItemsToCart: any;

    title: string = "Vue Mastery Socks";
    soxImage: string = "../assets/vmSocks-green-onWhite.jpg";
    inventory: number = 5;
    details: materialDetails[] = [
      {id: 1, material: "80% cotton"},
      {id: 2, material: "20% polyester"},
      {id: 3, material: "gender neutral"}
    ];
    colors: string[] = ["Green", "Blue"];
    soxColor: string = this.colors[0];

    handleAddToCart () {
      if(this.inventory > 0) {
        this.inventory--;
        this.handleItemsToCart();
      } else {
        alert('Product out of the stock')
      }
    }

    setSoxColor(color: string) {
      this.soxColor = color;
      console.log('sox color: ', this.soxColor);
    }

  }

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
