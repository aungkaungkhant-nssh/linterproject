<template>
  <div class="project" :class="{complete:project.complete}">
      <div class="flexing">
          <div>
            <h3 @click="showDetail">{{project.title}}</h3>
             <p v-if="hideDetail">{{project.detail}}</p>
          </div>
      
        <div>
          <span class="material-icons" @click="deleteProject">
            delete
             </span>
              <router-link :to="{name:'EditProject',params:{id:project.id}}">
                <span class="material-icons">
               edit
                </span>
              </router-link>
            
            <span class="material-icons" @click="completeProject">
                done
            </span>
         </div>
     </div>
  
  </div>
</template>

<script>
export default {
    props:['project'],
    data(){
        return{
            hideDetail:false,
            api:'http://localhost:3000/projects/',
        }
    },
    methods:{
        showDetail(){
            this.hideDetail=!this.hideDetail;
        },
        deleteProject(){
          let deleteRoute=this.api+this.project.id;
            fetch(deleteRoute,{method:"DELETE"})
            .then(()=>{
                this.$emit("delete",this.project.id)
            })
            .catch((err)=>{
                console.log(err);
            })
           
        },
        
        completeProject(){
             let completeRoute=this.api+this.project.id;
            fetch(completeRoute,{
                method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify({
                    complete:!this.project.complete,
                })
                })
                .then(()=>{
                    this.$emit("complete",this.project.id);
                })
                .catch(()=>{

                })
        }
    }
}
</script>

<style>
    .project{
        padding:20px;
        background-color: #f2f2f2;
        cursor: pointer;
        margin: 10px;
        border-left: 6px solid crimson;
        border-radius: 8px;
       
    }
    h3{
        color:indigo;
        width:120px;
        cursor: pointer;
    }
    .flexing{
        display: flex;
       justify-content: space-between;
        align-items: center;
    }
    span{
        margin-left:20px;
    }
    span:hover{
        color:#ccc
    }
    .complete{
         border-left: 6px solid green;
    }
</style>