<template>
  <select id="sort" name="sort" @change="$emit('sort-by', $event.target.value)">
    <option v-for="opt in options" :key="opt.value" :value="opt.value">
      {{ opt.label }}
    </option>
  </select>
</template>

<script>
export default {
  data: () => ({
    options: [
      {
        label: 'По умолчанию',
        value: 'default',
      },
      {
        label: 'По цене от меньшего к большему',
        value: 'minPrice',
      },
      {
        label: 'По цене от большего к меньшему',
        value: 'maxPrice',
      },
      {
        label: 'По наименованию',
        value: 'name',
      },
    ],
  }),
}
</script>

<style>
#sort {
  display: flex;
  align-items: center;
  justify-self: end;
  height: 36px;
  color: #b4b4b4;
  font-size: 12px;
  line-height: 15px;
  width: max-content;
  padding-left: 16px;
  background: #fffefb;
  box-shadow: 0 2px 5px rgb(0 0 0 / 10%);
  border-radius: 4px;
  border: none;
}
</style>
