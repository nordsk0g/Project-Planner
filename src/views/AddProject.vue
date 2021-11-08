<template>
  <form @submit.prevent="handleSubmit">
      <label for="title">Title:</label>
      <input v-model="title" type="text" name="title" id="title" required>
      <label for="details">Details:</label>
      <textarea v-model="details" name="details" id="details" required></textarea>
      <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
      return {
          title: null,
          details: null,
          uri: `http://localhost:3000/projects/`
      }
  },
  methods: {
      handleSubmit() {
        let project = {
          title: this.title,
          details: this.details,
          complete: false
        }
        fetch(this.uri, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(project)
        })
        .then(() => this.$router.push('/'))
        .catch(err => console.error(err.message))
      }
  }
}
</script>

<style>
    form {
    background: white;
    padding: 20px;
    border-radius: 10px;
  }
  label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 0.9em;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 1.25em 0 0.75em 0
  }
  input {
    padding: 0.75em;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 0.75em;
    width: 100%;
    box-sizing: border-box;
    height: 8em;
  }
  form button {
    display: block;
    margin: 1.25em auto 0;
    background: #00ce89;
    color: white;
    padding: 0.75em;
    border: 0;
    border-radius: 0.35em;
    font-size: 1em;
    cursor: pointer;
  }
</style>