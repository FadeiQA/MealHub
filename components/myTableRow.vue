<template>
  <tr @click="log">
    <td v-for="(column, id) in columns" :key="id">{{ column }}</td>
  </tr>
</template>

<script>
export default {
  name: 'MyTableRow',
  props: {
    columns: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    log() {
      this.$emit('click', '')
    },
  },
}
</script>
