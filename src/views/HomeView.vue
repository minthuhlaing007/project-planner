<template>
  <div class="home">
      <h1>Home Page</h1>
      <div v-for="project in projects" :key="project.id">
        <h3>{{ project.title }}</h3>
        <p>{{ project.detail }}</p>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      projects:[]
    }
  },
  mounted() {
    fetch("http://localhost:3000/projects")
    .then(response => response.json())
    .then(datas => this.projects = datas)
    .catch(error => console.log(error.message))
  }
}
</script>
