<template>
  <my-table :config="tableConfig" :data="comments" @click="goToComment"></my-table>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      comments: []
    }
  },
  computed: {
    tableConfig() {
      return {
        "id": "id",
        "name": "Имя",
        "email": "Почта",
      }
    },
  },
  mounted() {
    this.$axios.get("/api/comments")
      .then((result) => {
        this.comments = result.data
      })
  },
  methods: {
    goToComment(e) {
      this.$router.push(`/${e.id}`)
    }
  }
}

</script>
