<template>
  <div class="home">
    <FilterNav @updateFilter="handleUpdateFilter($event)" :currentFilter="currentFilter"/>

    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <Project :project="project" @delete="handleDelete" @complete="handleComplete"/>
      </div>
    </div>

    <div v-else>
      <p>Loading...</p>
    </div>

  </div>
</template>

<script>
import Project from '../components/Project.vue'
import FilterNav from '../components/FilterNav.vue'
import { computed } from '@vue/runtime-core'

export default {
  name: 'Home',
  components: {Project, FilterNav},
  data() {
    return {
      projects: [],
      currentFilter: 'all',
      filteredProjects: []
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter(project => project.id !== id)
    },
    handleComplete(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete 
    },
    handleUpdateFilter(event) {
      this.currentFilter = event
    }
  },
  computed: {
    filteredProjects() {
      if (this.currentFilter === 'done') {
        return this.projects.filter(project => project.complete)
      }
      if (this.currentFilter === 'todo') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  }
}
</script>
