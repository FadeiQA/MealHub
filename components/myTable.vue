<template>
  <div class="bd-example">
    <table class="table">
      <my-table-head :columns="tableHead" @click="sort"></my-table-head>
      <tbody>
        <my-table-row
          v-for="(row, keyRow) in tableRows"
          :key="keyRow"
          :columns="row.row"
          @click="goToDetails(row)"
        ></my-table-row>
      </tbody>
    </table>
    <div style="display: flex; flex-wrap: wrap">
      <span
        v-for="number in Math.ceil(data.length / 10)"
        :key="`number${number}`"
        :style="{
          background: +number - 1 === +page ? 'pink' : '',
          padding: '5px',
        }"
        @click="changePage(number)"
        >{{ number }}</span
      >
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyTable',
  props: {
    config: {
      type: Object,
      default: () => ({
        id: 'id',
        name: 'Имя',
        email: 'Почта',
      }),
    },
    data: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      sortBy: { key: '', direction: 'desc' },
      page: 0,
    }
  },
  computed: {
    tableHead() {
      return Object.values(this.config)
    },
    tableRows() {
      const keys = Object.keys(this.config)
      const items = [...this.data]
      items.sort((a, b) => {
        if (!this.sortBy.key || a[this.sortBy.key] === b[this.sortBy.key]) {
          return 0
        }
        if (a[this.sortBy.key] < b[this.sortBy.key]) {
          return this.sortBy.direction === 'desc' ? -1 : 1
        }
        return this.sortBy.direction === 'asc' ? -1 : 1
      })

      return items
        .map((item) => {
          return { meta: item, row: keys.map((key) => item[key]) }
        })
        .slice(this.page * 10, this.page * 10 + 10)
    },
  },
  methods: {
    sort(byKey) {
      const entries = Object.entries(this.config)
      if (this.sortBy.key === entries[byKey][0]) {
        this.sortBy.direction = this.sortBy.direction === 'asc' ? 'desc' : 'asc'
      } else {
        this.sortBy.direction = 'desc'
      }
      this.sortBy.key = entries[byKey][0]
    },
    changePage(number) {
      this.page = +number - 1
    },
    goToDetails(row) {
      this.$emit('click', row.meta)
    },
  },
}
</script>
