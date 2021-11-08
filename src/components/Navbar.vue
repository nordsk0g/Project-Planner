<template>
  <nav class="main-nav">
      <router-link :to="{ name: 'Home' }">Projects</router-link>
      <router-link :to="{ name: 'AddProject' }">Add a new project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
    .main-nav {
        text-align: center;
        margin: 2.5em;
    }
    .main-nav a {
        display: inline-block;
        text-decoration: none;
        margin: 0 0.75em;
        color: #999;
        font-size: 1.125em;
    }
    a.router-link-active {
        border-bottom: 0.125em solid #00ce89;
        padding-bottom: 0.25
    }
</style>