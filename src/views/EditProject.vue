<template>
  <form @submit.prevent="handleUpdate">
    <div v-if="title">
      <label for="title">Title:</label>
      <input v-model="title" type="text" name="title" id="title" required>
      <label for="details">Details:</label>
      <textarea v-model="details" name="details" id="details" required></textarea>
      <button>Update Project</button>
    </div>
  </form>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
        title: null,
        details: null,
        uri: `http://localhost:3000/projects/${this.id}`
    }
  },
  mounted() {
    fetch(this.uri)
    .then(res => res.json())
    .then(data => {
      this.title = data.title;
      this.details = data.details
    })
    .catch(err => console.error(err.message))
  },
  methods: {
    handleUpdate() {
      fetch(this.uri, { 
        method: 'PUT',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          title: this.title,
          details: this.details
        })
      })
      .then(() => this.$router.push('/'))
      .catch(err => console.error(err.message))
    }
  }
}
</script>

<style>

</style>