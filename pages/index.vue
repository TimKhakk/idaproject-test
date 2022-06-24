<template>
  <div class="container page-grid">
    <h1>Добавление товара</h1>
    <AddForm />
    <div class="product-list">
      <div v-for="item in productList" :key="item.id" class="product-item">
        <img :src="item.imgLink" />
        <div class="info">
          <span class="name">{{ item.name }}</span>
          <p class="descr">{{ item.descr }}</p>
          <span class="price">{{ item.price }} руб.</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AddForm from '~/components/AddForm.vue'
import productList from '~/constants/products.json'

export default {
  name: 'IndexPage',
  components: { AddForm },
  data: () => ({
    productList,
    formData: {
      name: '',
      descr: '',
      imgLink: '',
      price: '',
    },
  }),
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
.product-item {
  $dark-color: #3f3f3f;

  display: grid;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

  img {
    object-fit: cover;
    width: 100%;
    height: 200px;
  }

  .info {
    display: grid;
    gap: 16px;
    color: $dark-color;
    padding: 24px 16px;

    .name {
      font-weight: 600;
      font-size: 20px;
    }

    .descr {
      font-size: 16px;
      margin-bottom: 16px;
    }

    .price {
      font-weight: 600;
      font-size: 24px;
    }
  }
}
</style>
