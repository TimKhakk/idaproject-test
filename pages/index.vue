<template>
  <div class="container page-grid">
    <h1>Добавление товара</h1>
    <select id="sort" name="sort" @change="sortBy">
      <option value="default">По умолчанию</option>
      <option value="minPrice">По цене от меньшего к большему</option>
      <option value="maxPrice">По цене от большего к меньшему</option>
      <option value="name">По наименованию</option>
    </select>
    <AddForm @add-product="addProduct" />
    <ProductList :product-list="productList" :remove-product="removeProduct" />
  </div>
</template>

<script>
import AddForm from '~/components/AddForm.vue'
import productList from '~/constants/products.json'
import ProductList from '~/components/ProductList.vue'

export default {
  name: 'IndexPage',
  components: { AddForm, ProductList },
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
    sortBy(e) {
      const opt = e.target.value
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
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;
}
</style>
