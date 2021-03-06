<template>
  <div class="home">
    <h1>Home</h1>
    <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="projectDelete" @complete="projectComplete"></SingleProject>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject'
// @ is an alias to /src


export default {
  name: 'Home',
  components: {
    SingleProject,
   
  },
  data(){
    return{
      projects:[],
    }
  },
  mounted(){
    fetch("http://localhost:3000/projects")
    .then((response)=>{
      return response.json();
    })
    .then((datas)=>{
        this.projects=datas;
    })
    .catch((err)=>{
      console.log(err);
    })
  },
  methods:{
    projectDelete(id){
      this.projects=this.projects.filter((project) =>{
        return project.id!=id;
      })
    },
    projectComplete(id){
     let findProject=this.projects.find((project)=>{
       return project.id===id;
     })
     findProject.complete=!findProject.complete;
    }
  }
}
</script>
