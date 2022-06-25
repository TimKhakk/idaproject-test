<template>
  <div class="container page-grid">
    <h1>Добавление товара</h1>
    <AddForm @add-product="addProduct" />
    <div class="product-list">
      <ProductItem
        v-for="item in productList"
        :key="item.id"
        :item="item"
        @remove-product="removeProduct"
      />
    </div>
  </div>
</template>

<script>
import AddForm from '~/components/AddForm.vue'
import productList from '~/constants/products.json'
import ProductItem from '~/components/ProductItem.vue'

export default {
  name: 'IndexPage',
  components: { AddForm, ProductItem },
  data: () => ({
    productList,
    formData: {
      name: '',
      descr: '',
      imgLink: '',
      price: '',
    },
  }),
  methods: {
    addProduct(item) {
      this.productList.push(item)
    },
    removeProduct(id) {
      this.productList = this.productList.filter((item) => item.id !== id)
    },
  },
}
</script>

<style lang="scss">
.container {
  display: grid;
  width: 1360px;
  margin: 0 auto;
  padding: 32px 16px;
}

.page-grid {
  display: grid;
  grid-template-columns: 332px 1fr;
  grid-template-rows: max-content max-content;
  align-items: start;
  gap: 16px;
}

h1 {
  grid-column: span 2;
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
}

.product-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
</style>
