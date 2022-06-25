<template>
  <div class="product-list">
    <ProductItem
      v-for="item in productList"
      :key="item.id"
      :item="item"
      @remove-product="removeProduct"
    />
  </div>
</template>

<script>
import ProductItem from '~/components/ProductItem.vue'

export default {
  name: 'ProductList',
  components: { ProductItem },
  props: {
    productList: {
      type: Array,
      required: true,
    },
    removeProduct: {
      type: Function,
      required: true,
    },
  },
}
</script>

<style>
.product-list {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  gap: 16px;
}
@media only screen and (min-width: 640px) {
  .product-list {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media only screen and (min-width: 768px) {
  .product-list {
    grid-template-columns: repeat(1, 1fr);
  }
}
@media only screen and (min-width: 940px) {
  .product-list {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media only screen and (min-width: 1400px) {
  .product-list {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
