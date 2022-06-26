<template>
  <label>
    <select
      id="sort"
      name="sort"
      @change="$emit('sort-by', $event.target.value)"
    >
      <option v-for="opt in options" :key="opt.value" :value="opt.value">
        {{ opt.label }}
      </option>
    </select>
    <svg
      class="btn"
      width="8"
      height="6"
      viewBox="0 0 8 6"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        d="M7.48532 1.24264L4.24268 4.48528L1.00003 1.24264"
        stroke="#B4B4B4"
      />
    </svg>
  </label>
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
        label: 'От мен. к бол.',
        value: 'minPrice',
      },
      {
        label: 'От бол. к мен.',
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

<style lang="scss" scoped>
label {
  display: flex;
  justify-self: end;
  align-items: center;
  position: relative;
}
.btn {
  position: absolute;
  right: 16px;
}
#sort {
  display: flex;
  align-items: center;
  justify-self: end;
  position: relative;
  appearance: none;
  height: 36px;
  color: #b4b4b4;
  font-size: 12px;
  line-height: 15px;
  width: max-content;
  padding-left: 16px;
  padding-right: 32px;
  background: #fffefb;
  box-shadow: 0 2px 5px rgb(0 0 0 / 10%);
  border-radius: 4px;
  border: none;

  option {
    color: #49485e;
  }
}
</style>
