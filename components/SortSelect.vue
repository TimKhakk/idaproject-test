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
