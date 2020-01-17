<template>
  <div class="product-page__container">
    <div class="product-page__leftcol">
      <img
        class="product-page__product-image"
        :src="activeVariant.image"
      >
    </div>
    <div class="product-page__rightcol">
      <h1>{{title}}</h1>
      <span>Shipping: 24 hours</span>
      <span :style="[isInStock ? {color: 'green'} : {color: 'red'}]">
        Stock: {{activeVariant.inventory}}
      </span>
      <h2>Details</h2>
      <ul>
        <li v-for="detail in activeVariant.details" v-bind:key="detail.id">{{detail.description}}</li>
      </ul>
      <div class="product-page__color-option"></div>
      <h2>Colors:</h2>
      <div
        v-for="(variant, index) in productVariants"
        :key="variant.id"
        class="variant-box"
        :style="{backgroundColor: variant.color}"
        v-on:click="setActiveVariant(index)"
      >
      </div>
      <button
        v-on:click="handleAddToCart(activeVariant.id)"
        :disabled="!isInStock"
      >Add to Cart
      </button>
      <button
        v-on:click="handleRemoveFromCart(activeVariant.id)"
      >Remove from cart
      </button>

      <h2>Add product review</h2>
      <ProductReview />

    </div>

  </div>
</template>

<script lang="ts">
import {Component, Vue} from 'vue-property-decorator';
import ProductReview from "@/components/ProductReview.vue";

interface MaterialDetails {
  id: number;
  description: string;
}

interface ProductVariant {
  id: number;
  color: string;
  image: string;
  inventory: number;
  details: MaterialDetails[];
}

Component.registerHooks([
  'created',
]);
@Component({
  components: {ProductReview}
})
export default class ProductPage extends Vue {
  brand: string = "Vue Mastery";
  product: string = "Sox";
  activeVariant: ProductVariant | null = null;
  productVariants: ProductVariant[] = [
    {
      id: 234,
      color: "Green",
      image: "./images/green.jpg",
      inventory: 10,
      details: [
        {id: 1, description: "80% cotton"},
        {id: 2, description: "20% polyester"},
        {id: 3, description: "gender neutral"}
      ]
    },
    {
      id: 456,
      color: "Blue",
      image: "./images/blue.jpg",
      inventory: 5,
      details: [
        {id: 1, description: "99% cotton"},
        {id: 2, description: "1% polyester"},
        {id: 3, description: "gender neutral"}
      ]
    }
  ];

  created() {
    this.setActiveVariant(0);
  }

  setActiveVariant(index: number = 0): void {
    this.activeVariant = this.productVariants[index];
  }

  handleAddToCart(id: number): void {
    if (this.activeVariant!.inventory > 0) {
      this.activeVariant!.inventory--;
      this.$emit('add-to-cart', id);
    }
  }

  handleRemoveFromCart(id: number): void {
    this.activeVariant!.inventory++;
    this.$emit('remove-from-cart', id);
  }

  get title(): string {
    return this.brand + " " + this.product;
  }

  get isInStock(): boolean {
    if (this.activeVariant !== null) {
      return !!this.activeVariant.inventory;
    }
    return false;
  }


}

</script>

<style lang="scss" scoped>


.product-page__container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.product-page__leftcol {
  display: flex;
  justify-content: center;
  align-items: center;

}

.product-page__product-image {
  max-width: 500px;
}

.product-page__rightcol {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.variant-box {
  width: 50px;
  height: 50px;
  margin-top: 5px;
  border-radius: 50%;
  cursor: pointer;
}

.variant-box:last-of-type {
  margin-bottom: 30px;
}

button {
  margin-bottom:20px;
}

</style>
