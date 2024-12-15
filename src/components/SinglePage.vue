<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="flexing">
      <div>
        <h3 @click="showDetail = !showDetail">{{ project.title }}</h3>
      </div>
      <div>
        <span class="material-icons" @click="deleteProject">delete</span>
        <span class="material-icons">edit</span>
        <span class="material-icons" @click="completeProject">done</span>
      </div>
    </div>
    <div v-if="showDetail">
      <p>{{ project.detail }}</p>
    </div>
    <p>{{ project.complete }}</p>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetail: false,
      api: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    deleteProject() {
      fetch(this.api, { method: "DELETE" })
        .then(() => {
          this.$emit("delete", this.project.id);
        })
        .catch((error) => console.log(error.message));
    },
    completeProject() {
      let updataCompleteRoute = this.api;
      fetch(updataCompleteRoute, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          complete: !this.project.complete,
        }),
      })
      .then(()=>{
        this.$emit("complete",this.project.complete)
      })
      .catch(error=>console.log(error.message));
    },
  },
};
</script>

<style>
.project {
  padding: 20px;
  background-color: #f2f2f2;
  margin: 10px;
  border-left: 10px solid crimson;
  border-radius: 20px;
}

h3 {
  color: indigo;
  cursor: pointer;
}
.flexing {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
span {
  margin-left: 25px;
}
span:hover {
  color: red;
  cursor: pointer;
}
.complete {
  border-left-color: green;
}
</style>
