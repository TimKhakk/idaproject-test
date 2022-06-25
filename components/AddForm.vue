<template>
  <form class="form-wrapper">
    <label>
      <span class="title">Наименование товара</span>
      <input required placeholder="Введите наименование товара" type="text" />
      <span class="error-message">Поле является обязательным</span>
    </label>
    <label>
      <span>Описание товара</span>
      <textarea
        id="descr"
        placeholder="Введите описание товара"
        name="descr"
        cols="30"
        rows="10"
      ></textarea>
    </label>
    <label>
      <span class="title">Ссылка на изображение товара</span>
      <input required placeholder="Введите ссылку" type="url" name="link" />
      <span class="error-message">Поле является обязательным</span>
    </label>
    <label>
      <span class="title">Цена товара</span>
      <input required placeholder="Введите цену" type="number" />
      <span class="error-message">Поле является обязательным</span>
    </label>
    <button type="submit">Добавить товар</button>
  </form>
</template>
<script>
export default {
  name: 'AddForm',
}
</script>
<style lang="scss">
$white: #fffefb;
$dark-blue: #49485e;

.form-wrapper {
  $tomato: #ff8484;

  display: grid;
  row-gap: 16px;

  width: 284px;
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

      &:invalid {
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
    }

    input:invalid + .error-message {
      opacity: 1;
    }
  }
}

button {
  $active: #7bae73;

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
    background: #eeeeee;
    color: #b4b4b4;
  }
}
</style>
