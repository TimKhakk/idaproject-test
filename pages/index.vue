<template>
  <div class="container page-grid">
    <h1>Добавление товара</h1>
    <SortSelect @sort-by="sortBy" />
    <AddForm @add-product="addProduct" />
    <template v-if="loading">
      <ProductListSkeleton />
    </template>
    <ProductList
      v-else-if="productList.length > 0"
      :product-list="productList"
      :remove-product="removeProduct"
    />
    <p v-else class="empty-text">Товары не найдены.</p>
  </div>
</template>

<script>
import ProductListSkeleton from '../components/ProductListSkeleton.vue'
import AddForm from '~/components/AddForm.vue'
import productList from '~/constants/products.json'
import ProductList from '~/components/ProductList.vue'
import SortSelect from '~/components/SortSelect.vue'

export default {
  name: 'IndexPage',
  components: { AddForm, ProductList, SortSelect, ProductListSkeleton },
  data: () => ({
    loading: true,
    productList: [],
  }),
  beforeMount() {
    if (localStorage.getItem('product-list-vue')) {
      this.productList = JSON.parse(localStorage.getItem('product-list-vue'))
    } else {
      localStorage.setItem('product-list-vue', JSON.stringify(productList))
      this.productList = productList
    }
    this.loading = false
  },
  methods: {
    addProduct(item) {
      this.productList.unshift(item)
      localStorage.setItem('product-list-vue', JSON.stringify(this.productList))
    },
    removeProduct(id) {
      this.productList = this.productList.filter((item) => item.id !== id)
      localStorage.setItem('product-list-vue', JSON.stringify(this.productList))
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
        this.productList.sort((a, b) => b.id - a.id)
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
.empty-text {
  font-size: 20;
  font-weight: 600;
  text-align: center;
}
</style>
