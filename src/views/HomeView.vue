<template>
  <div class="home">
      <h1>Home Page</h1>
      <div v-for="project in projects" :key="project.id">
        <SinglePage :project="project"></SinglePage>
      </div>
  </div>
</template>

<script>
import SinglePage from '../components/SinglePage'
export default {
  components: { SinglePage },
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
