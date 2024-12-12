<template>
  <div class="project">
    <div class="flexing">
      <div>
        <h3 @click="showDetail =! showDetail">{{ project.title }}</h3>
      </div>
      <div>
        <span class="material-icons" @click="deleteProject">delete</span>
        <span class="material-icons">edit</span>
        <span class="material-icons">done</span>
      </div>
    </div>
    <div v-if="showDetail">
      <p>{{ project.detail }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return{
      showDetail:false,
      api: "http://localhost:3000/projects/"+this.project.id
    }
  },
  methods:{
    deleteProject(){
      fetch(this.api,{method:"DELETE"})
      .then(()=>{
        this.$emit("delete",this.project.id)
      })
      .catch(error=>console.log(error.message))
    }
  }
};
</script>

<style>
.project {
  padding: 20px;
  background-color: #f2f2f2;
  margin: 10px;
  border-left: 4px solid crimson;
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
span{
  margin-left: 25px;
}
span:hover{
  color: red;
  cursor: pointer;
}
</style>
