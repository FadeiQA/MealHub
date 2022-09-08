<template>
  <thead>
  <tr>
    <th @click="$emit(`click`, id)" v-for="(column, id) in columns" :key="id"> {{ column }} </th>
  </tr>
  </thead>
</template>

<script>
export default {
  name: "MyTableHead",
  props: {
    columns: {
      type: Array,
      default: () => []
    }
  },
}
</script>

