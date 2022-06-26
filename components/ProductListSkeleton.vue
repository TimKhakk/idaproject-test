<template>
  <div class="product-list-skeleton">
    <div
      v-for="key in [1, 2, 3, 4, 5, 6]"
      :key="key"
      class="product-item-skeleton"
    >
      <div class="grid loader"></div>
      <div class="info">
        <span class="name loader"></span>
        <p class="descr loader"></p>
        <span class="price loader"></span>
      </div>
    </div>
  </div>
</template>
<style lang="scss">
.product-list-skeleton {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  gap: 16px;
}

.loader {
  overflow: hidden;
  position: relative;
  background-color: #e2e2e2;
  border-radius: 4px;

  &.card-image {
    border-radius: 0;
  }

  &::after {
    display: block;
    border-radius: 4px;
    content: '';
    position: absolute;
    width: 100%;
    height: 100%;
    transform: translateX(-100%);
    background: linear-gradient(
      90deg,
      transparent,
      rgba(255, 255, 255, 0.2),
      transparent
    );
    animation: loader 1.5s infinite;
  }
}

@keyframes loader {
  100% {
    transform: translateX(100%);
  }
}

@media only screen and (min-width: 640px) {
  .product-list-skeleton {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media only screen and (min-width: 768px) {
  .product-list-skeleton {
    grid-template-columns: repeat(1, 1fr);
  }
}
@media only screen and (min-width: 940px) {
  .product-list-skeleton {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media only screen and (min-width: 1400px) {
  .product-list-skeleton {
    grid-template-columns: repeat(3, 1fr);
  }
}
.product-item-skeleton {
  $dark-color: #3f3f3f;
  max-width: 340px;

  display: grid;
  grid-template-rows: 200px 1fr;
  position: relative;
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

  img {
    object-fit: cover;
    width: 100%;
    height: 200px;
  }

  .info {
    display: grid;
    grid-template-rows: max-content 1fr max-content;
    gap: 16px;
    color: $dark-color;
    padding: 24px 16px;

    .name {
      width: 70%;
      height: 25px;
    }

    .descr {
      min-height: 80px;
    }

    .price {
      height: 31px;
      width: 40%;
    }
  }
}
</style>
