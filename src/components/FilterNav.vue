
   
<template>
  <nav class="filter-nav">
    <button 
      @click="updateFilter('all')" 
      :class="{active: currentFilter === 'all'}"
    >View all</button>
    <button 
      @click="updateFilter('done')"
      :class="{active: currentFilter === 'done'}"
    >Done</button>
    <button 
      @click="updateFilter('todo')"
      :class="{active: currentFilter === 'todo'}"
    >To Do</button>
  </nav>
</template>

<script>
export default {
  props: ['currentFilter'],
  methods: {
    updateFilter(by) {
      this.$emit('updateFilter', by)
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
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
  }
  .filter-nav button.active {
    color: #555;
  }
</style>