<template>
  <div class="container page-grid">
    <h1>Добавление товара</h1>
    <SortSelect @sort-by="sortBy" />
    <AddForm @add-product="addProduct" />
    <ProductList :product-list="productList" :remove-product="removeProduct" />
  </div>
</template>

<script>
import AddForm from '~/components/AddForm.vue'
import productList from '~/constants/products.json'
import ProductList from '~/components/ProductList.vue'
import SortSelect from '~/components/SortSelect.vue'
import 'animate.css'

export default {
  name: 'IndexPage',
  components: { AddForm, ProductList, SortSelect },
  data: () => ({
    productList,
  }),
  methods: {
    addProduct(item) {
      this.productList.push(item)
    },
    removeProduct(id) {
      this.productList = this.productList.filter((item) => item.id !== id)
    },
    sortBy(opt) {
      if (opt === 'name') {
        this.productList.sort((a, b) => {
          const nameA = a.name.toLowerCase()
          const nameB = b.name.toLowerCase()
          if (nameA < nameB) return -1
          if (nameA > nameB) return 1
          return 0
        })
      }
      if (opt === 'minPrice') {
        this.productList.sort((a, b) => a.price - b.price)
      }
      if (opt === 'maxPrice') {
        this.productList.sort((a, b) => b.price - a.price)
      }
      if (opt === 'default') {
        this.productList.sort((a, b) => a.id - b.id)
      }
    },
  },
}
</script>

<style lang="scss">
h1 {
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
}
</style>
