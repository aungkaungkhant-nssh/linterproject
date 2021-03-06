<template>
  <div class="project">
      <div class="flexing">
          <div>
            <h3 @click="showDetail">{{project.title}}</h3>
             <p v-if="hideDetail">{{project.detail}}</p>
          </div>
      
        <div>
          <span class="material-icons">
            delete
             </span>
         <span class="material-icons">
            edit
            </span>
            <span class="material-icons">
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
            hideDetail:false
        }
    },
    methods:{
        showDetail(){
            this.hideDetail=!this.hideDetail;
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
</style>