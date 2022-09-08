<template>
  <div>
    <h2>{{ commentData?.name }}</h2>
    <h3>id коммента: {{ commentData?.id }}</h3>
    <h4>id поста: {{ commentData?.postId }}</h4>
    <h5>email: {{ commentData?.email }}</h5>
    <br />
    <br />
    <section>{{ commentData?.body }}</section>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      commentData: {},
    }
  },
  computed: {
    tableConfig() {
      return {
        id: 'id',
        name: 'Имя',
        email: 'Почта',
      }
    },
  },
  mounted() {
    this.$axios.get(`/comments/${this.$route.params.id}`).then((result) => {
      this.commentData = result.data
    })
  },
}
</script>
