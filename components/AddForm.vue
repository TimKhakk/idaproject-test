<template>
  <form class="form-wrapper">
    <label>
      <span class="title">Наименование товара</span>
      <input
        v-model.trim="formData.name"
        required
        placeholder="Введите наименование товара"
        type="text"
      />
      <span class="error-message">Поле является обязательным</span>
    </label>
    <label>
      <span>Описание товара</span>
      <textarea
        id="descr"
        v-model.trim="formData.descr"
        placeholder="Введите описание товара"
        name="descr"
        cols="30"
        rows="10"
      ></textarea>
    </label>
    <label>
      <span class="title">Ссылка на изображение товара</span>
      <input
        v-model.trim="formData.imgLink"
        required
        placeholder="Введите ссылку"
        type="url"
        name="imgLink"
      />
      <span class="error-message">Поле является обязательным</span>
    </label>
    <label>
      <span class="title">Цена товара</span>
      <input
        v-model.trim.number="formData.price"
        required
        placeholder="Введите цену"
        type="number"
      />
      <span class="error-message">Поле является обязательным</span>
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
    formData: {
      name: '',
      descr: '',
      imgLink: '',
      price: '',
    },
  }),
  computed: {
    isDisabledSubmitBtn() {
      if (!this.formData.name) return true
      if (!this.formData.imgLink) return true
      if (!this.formData.price) return true
      return false
    },
  },
  methods: {
    handleSubmit() {
      const newItem = {
        id: Date.now(),
        name: this.formData.name,
        descr: this.formData.descr,
        price: this.formData.price,
        imgLink: this.formData.imgLink,
      }
      this.formData.name = ''
      this.formData.descr = ''
      this.formData.price = ''
      this.formData.imgLink = ''

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

      // &:invalid {
      //   outline: 1px solid $tomato;
      // }
    }

    .error-message {
      position: absolute;
      opacity: 0;
      bottom: -14px;
      position: absolute;
      font-size: 8px;
      content: '';
      color: $tomato;
    }

    // input:invalid + .error-message {
    //   opacity: 1;
    // }
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
