<template>
  <div class="home">
    <h1>Home Page</h1>
    <div v-for="project in projects" :key="project.id">
      <SinglePage
        :project="project"
        @delete="deletePage"
        @complete="completeProject"
      ></SinglePage>
    </div>
  </div>
</template>

<script>
import SinglePage from "../components/SinglePage";
export default {
  components: { SinglePage },
  data() {
    return {
      projects: [],
    };
  },
  methods: {
    deletePage(id) {
      this.projects = this.projects.filter((project) => {
        return project.id != id;
      });
    },
    completeProject(id) {
      let findProject = this.projects.find((project) => {
        return project.id === id;
      });
      findProject.complete = !findProject.complete;
    },
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((response) => response.json())
      .then((datas) => (this.projects = datas))
      .catch((error) => console.log(error.message));
  },
};
</script>
