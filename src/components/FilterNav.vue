<template>
  <nav class="filter-nav">
    <button 
    @click="updateFilter('all')"
    :class="{ active: currentFilter === 'all'}"
    >View All</button>
    <button 
    @click="updateFilter('completed')"
    :class="{ active: currentFilter === 'completed'}"
    >Completed</button>
    <button 
    @click="updateFilter('ongoing')"
    :class="{ active: currentFilter === 'ongoing'}"
    >Ongoing</button>
  </nav>
</template>

<script>
export default {
  props: ['currentFilter'],
  methods: {
    updateFilter(term) {
      this.$emit('filterChange', term)
    }
  }
}
</script>

<style>
  .filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 0.75em;
    text-transform: uppercase;
    margin-right: 0.65em;
    letter-spacing: 0.1em;
    font-weight: bold;
    cursor: pointer;
  }

  .filter-nav button.active {
    color: #555;
  }
</style>