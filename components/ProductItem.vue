<template>
  <div class="product-item">
    <div class="grid">
      <img :src="item.imgLink" :alt="item.name" />
    </div>
    <div class="info">
      <span class="name">{{ item.name }}</span>
      <p class="descr">{{ item.descr | descr }}</p>
      <span class="price">{{ item.price | price }} руб.</span>
    </div>

    <button class="delete-item" @click="$emit('remove-product', item.id)">
      <svg
        width="16"
        height="16"
        viewBox="0 0 16 16"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g clip-path="url(#clip0_4_349)">
          <path
            d="M10.207 5.79688C9.99998 5.79688 9.83224 5.96462 9.83224 6.17158V13.2535C9.83224 13.4604 9.99998 13.6283 10.207 13.6283C10.4139 13.6283 10.5817 13.4604 10.5817 13.2535V6.17158C10.5817 5.96462 10.4139 5.79688 10.207 5.79688Z"
            fill="white"
          />
          <path
            d="M5.78544 5.79688C5.57848 5.79688 5.41074 5.96462 5.41074 6.17158V13.2535C5.41074 13.4604 5.57848 13.6283 5.78544 13.6283C5.99241 13.6283 6.16015 13.4604 6.16015 13.2535V6.17158C6.16015 5.96462 5.99241 5.79688 5.78544 5.79688Z"
            fill="white"
          />
          <path
            d="M2.56294 4.76335V13.9953C2.56294 14.541 2.76303 15.0534 3.11256 15.4211C3.46048 15.7898 3.94467 15.9991 4.4514 16H11.541C12.0478 15.9991 12.532 15.7898 12.8798 15.4211C13.2293 15.0534 13.4294 14.541 13.4294 13.9953V4.76335C14.1242 4.57893 14.5745 3.90768 14.4815 3.19471C14.3884 2.48189 13.7811 1.94867 13.0622 1.94852H11.1437V1.48014C11.1459 1.08626 10.9902 0.708039 10.7113 0.42979C10.4325 0.151688 10.0537 -0.0031709 9.65982 4.92333e-05H6.33255C5.93867 -0.0031709 5.55986 0.151688 5.28103 0.42979C5.00219 0.708039 4.84646 1.08626 4.84865 1.48014V1.94852H2.93019C2.21122 1.94867 1.60393 2.48189 1.51084 3.19471C1.4179 3.90768 1.86813 4.57893 2.56294 4.76335ZM11.541 15.2506H4.4514C3.81075 15.2506 3.31236 14.7002 3.31236 13.9953V4.79629H12.68V13.9953C12.68 14.7002 12.1816 15.2506 11.541 15.2506ZM5.59806 1.48014C5.59558 1.28503 5.67227 1.09724 5.81074 0.959502C5.94906 0.821768 6.13729 0.746095 6.33255 0.749461H9.65982C9.85508 0.746095 10.0433 0.821768 10.1816 0.959502C10.3201 1.09709 10.3968 1.28503 10.3943 1.48014V1.94852H5.59806V1.48014ZM2.93019 2.69793H13.0622C13.4347 2.69793 13.7367 2.99989 13.7367 3.3724C13.7367 3.74491 13.4347 4.04688 13.0622 4.04688H2.93019C2.55768 4.04688 2.25571 3.74491 2.25571 3.3724C2.25571 2.99989 2.55768 2.69793 2.93019 2.69793Z"
            fill="white"
          />
          <path
            d="M7.9962 5.79688C7.78923 5.79688 7.62149 5.96462 7.62149 6.17158V13.2535C7.62149 13.4604 7.78923 13.6283 7.9962 13.6283C8.20317 13.6283 8.37091 13.4604 8.37091 13.2535V6.17158C8.37091 5.96462 8.20317 5.79688 7.9962 5.79688Z"
            fill="white"
          />
        </g>
        <defs>
          <clipPath id="clip0_4_349">
            <rect width="16" height="16" fill="white" />
          </clipPath>
        </defs>
      </svg>
    </button>
  </div>
</template>

<script>
import chunk from 'lodash.chunk'
export default {
  name: 'ProductItem',
  filters: {
    price(val) {
      const arr = val.toString().split('').reverse()
      return chunk(arr, 3)
        .map((i) => i.reverse().join(''))
        .reverse()
        .join(' ')
    },
    descr(val) {
      let res = val
      if (val.length > 135) {
        res = res.slice(0, 135) + '...'
      }
      return res
    },
  },
  props: {
    item: {
      type: Object,
      require: true,
      default: () => ({
        name: '',
        imgLink: '',
        descr: '',
        price: 0,
      }),
    },
  },
}
</script>

<style lang="scss">
.product-item {
  $dark-color: #3f3f3f;
  max-width: 340px;

  display: grid;
  background: #fffefb;
  grid-template-rows: 200px 1fr;
  position: relative;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;

  &-move,
  &-enter-active,
  &-leave-active {
    transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
  }

  &-enter-from,
  &-leave-to {
    z-index: -1;
    opacity: 0 !important;
    transform: scaleY(0.5) translate(0, 10px) !important;
  }

  &-leave-active {
    position: absolute !important;
  }

  &:hover .delete-item {
    opacity: 1;
    pointer-events: all;
  }
  @media only screen and (hover: none) and (pointer: coarse) {
    .delete-item {
      opacity: 1 !important;
      pointer-events: all !important;
    }
  }

  .delete-item {
    opacity: 0;
    pointer-events: none;
    transition: all 0.2s ease-in-out;
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: -5px;
    right: -5px;
    background: #ff8484;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    width: 32px;
    height: 32px;
    border: none;

    &:hover {
      background: #f87171;
      transform: scale(1.05);
    }

    &:active {
      background: rgb(248, 128, 128);
    }
  }

  img {
    object-fit: cover;
    width: 100%;
    height: 200px;
    background: #eeeeee;
  }

  .info {
    display: grid;
    grid-template-rows: max-content 1fr max-content;
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
      min-height: 80px;
    }

    .price {
      font-weight: 600;
      font-size: 24px;
    }
  }
}
</style>
