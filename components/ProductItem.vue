<template>
  <div class="product-item">
    <img :src="item.imgLink" />
    <div class="info">
      <span class="name">{{ item.name }}</span>
      <p class="descr">{{ item.descr }}</p>
      <span class="price">{{ item.price }} руб.</span>
    </div>

    <button class="delete-item" @click="$emit('remove-product', item.id)">
      Delete
    </button>
  </div>
</template>

<script>
export default {
  name: 'ProductItem',
  props: {
    item: {
      type: Object,
      require: true,
      default: () => ({
        name: '',
        imgLink: '',
        descr: '',
        price: '',
      }),
    },
  },
}
</script>

<style lang="scss">
.product-item {
  $dark-color: #3f3f3f;

  display: grid;
  background: #fffefb;
  position: relative;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

  &:hover .delete-item {
    display: flex;
  }

  .delete-item {
    display: none;
    position: absolute;
  }

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
