<template>
  <thead>
    <tr>
      <th v-for="(column, id) in columns" :key="id" @click="$emit(`click`, id)">
        {{ column }}
      </th>
    </tr>
  </thead>
</template>

<script>
export default {
  name: 'MyTableHead',
  props: {
    columns: {
      type: Array,
      default: () => [],
    },
  },
}
</script>
