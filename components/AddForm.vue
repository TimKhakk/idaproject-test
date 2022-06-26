<template>
  <form class="form-wrapper">
    <label>
      <span class="title">Наименование товара</span>
      <input
        v-model.trim="form.name.value"
        :class="{ error: form.name.touched && form.name.value === '' }"
        required
        placeholder="Введите наименование товара"
        type="text"
        @blur="form.name.touched = true"
      />
      <span
        class="error-message"
        :class="{
          show: form.name.touched && form.name.value === '',
        }"
        >Поле является обязательным</span
      >
    </label>
    <label>
      <span>Описание товара</span>
      <textarea
        id="descr"
        v-model.trim="form.descr.value"
        placeholder="Введите описание товара"
        name="descr"
        cols="30"
        rows="10"
      ></textarea>
    </label>
    <label>
      <span class="title">Ссылка на изображение товара</span>
      <input
        v-model.trim="form.imgLink.value"
        :class="{ error: form.imgLink.touched && form.imgLink.value === '' }"
        required
        placeholder="Введите ссылку"
        type="url"
        name="imgLink"
        @blur="form.imgLink.touched = true"
      />
      <span
        class="error-message"
        :class="{
          show: form.imgLink.touched && form.imgLink.value === '',
        }"
        >Поле является обязательным</span
      >
    </label>
    <label>
      <span class="title">Цена товара</span>
      <input
        v-model.trim.number="form.price.value"
        :class="{ error: form.price.touched && form.price.value === '' }"
        required
        placeholder="Введите цену"
        type="number"
        @blur="form.price.touched = true"
      />
      <span
        class="error-message"
        :class="{
          show: form.price.touched && form.price.value === '',
        }"
        >Поле является обязательным</span
      >
    </label>
    <button
      :disabled="isDisabledSubmitBtn"
      type="submit"
      @click.prevent="handleSubmit"
    >
      Добавить товар
    </button>
  </form>
</template>
<script>
export default {
  name: 'AddForm',
  data: () => ({
    form: {
      name: {
        value: '',
        touched: false,
      },
      descr: {
        value: '',
        touched: false,
      },
      imgLink: {
        value: '',
        touched: false,
      },
      price: {
        value: '',
        touched: false,
      },
    },
  }),
  computed: {
    isDisabledSubmitBtn() {
      if (!this.form.name.value) return true
      if (!this.form.imgLink.value) return true
      if (!this.form.price.value) return true
      return false
    },
  },
  methods: {
    handleSubmit() {
      const newItem = {
        id: Date.now(),
        name: this.form.name.value,
        descr: this.form.descr.value,
        price: this.form.price.value,
        imgLink: this.form.imgLink.value,
      }
      this.form.name.value = ''
      this.form.name.touched = false
      this.form.descr.value = ''
      this.form.descr.touched = false
      this.form.price.value = ''
      this.form.price.touched = false
      this.form.imgLink.value = ''
      this.form.imgLink.touched = false

      this.$emit('add-product', newItem)
    },
  },
}
</script>

<style lang="scss">
$white: #fffefb;
$dark-blue: #49485e;

.form-wrapper {
  $tomato: #ff8484;

  display: grid;
  row-gap: 16px;
  border-radius: 4px;
  background: $white;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  padding: 24px;

  label {
    display: grid;
    row-gap: 4px;
    position: relative;

    span {
      color: $dark-blue;
      font-size: 10px;
      position: relative;

      &.title::after {
        content: '';
        position: absolute;
        width: 4px;
        height: 4px;
        border-radius: 50%;
        background: $tomato;
      }
    }

    textarea {
      resize: none;
      height: 108px;
      min-height: 40px;
      max-height: 180px;
    }

    input,
    textarea {
      position: relative;
      background: $white;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      padding: 10px 16px 11px;
      font-size: 12px;
      border: none;

      &.error {
        outline: 1px solid $tomato;
      }
    }

    .error-message {
      position: absolute;
      opacity: 0;
      bottom: -14px;
      position: absolute;
      font-size: 8px;
      content: '';
      color: $tomato;

      &.show {
        opacity: 1;
      }
    }
  }

  button {
    $active: #7bae73;

    transition: background 0.2s ease-in-out;
    margin-top: 8px;
    height: 36px;
    border-radius: 10px;
    font-weight: 600;
    font-size: 12px;
    border: none;
    background: $active;
    color: white;

    &:disabled {
      cursor: initial;
      background: #eeeeee !important;
      color: #b4b4b4;
    }

    &:hover {
      background: #53a945;
    }

    &:active {
      background: rgb(123, 175, 114);
    }
  }
}

@media only screen and (min-width: 768px) {
  .form-wrapper {
    width: 284px;
  }
}
</style>
