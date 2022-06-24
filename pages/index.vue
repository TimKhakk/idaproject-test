<template>
  <div class="container">
    <h1>Добавление товара</h1>
    <AddForm />
  </div>
</template>

<script>
import AddForm from '~/components/AddForm.vue'
export default {
  name: 'IndexPage',
  components: { AddForm },
}
</script>

<style lang="scss">
.container {
  display: grid;
  width: 1170px;
  margin: 0 auto;
  padding: 32px 0;
}

h1 {
  font-weight: bold;
  font-size: 28px;
  line-height: 35px;
  margin-bottom: 16px;
}
</style>
