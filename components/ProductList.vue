<template>
  <transition-group class="product-list" name="product-list" tag="div">
    <ProductItem
      v-for="item in productList"
      :key="item.id"
      :item="item"
      @remove-product="removeProduct"
    />
  </transition-group>
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

<style lang="scss">
.product-list {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  gap: 16px;

  &-move,
  &-enter-active,
  &-leave-active {
    transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
  }

  &-enter-from,
  &-leave-to {
    z-index: -1;
    opacity: 0;
    transform: scaleY(0.5) translate(0, 10px);
  }

  &-leave-active {
    position: absolute;
  }
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
