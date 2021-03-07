<template>
   <h1>Edit Project</h1>
    <form @submit.prevent="editProject">
        <label>Project Title</label>
      <input type="text" v-model="title">
      <label>Project Detail</label>
      <input type="text" v-model="detail">
      <button>Edit Project</button>
    </form>
</template>

<script>
export default {
    data(){
        return{
            title:"",
            detail:"",
        }
    },
   props:["id"],
   mounted(){
       fetch("http://localhost:3000/projects/"+this.id)
       .then((response)=>{
           return response.json();
       })
       .then((datas)=>{
           this.title=datas.title,
           this.detail=datas.detail
       })
       .catch((error)=>{
           console.log(error);
       })
   },
   methods:{
       editProject(){
            fetch("http://localhost:3000/projects/"+this.id,{
                method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify({
                    title:this.title,
                    detail:this.detail
                })
            })
            .then(()=>{
                this.$router.push("/");
            })
            .catch((error)=>{
                console.log(error);
            })
       }
   }
}
</script>

<style>

</style>