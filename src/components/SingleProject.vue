<template>
  <div class="project">
      <h3 @click="showDetail">{{project.title}}</h3>
      <p v-if="hideDetail">{{project.detail}}</p>
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
        background-color: #ccc;
        width:400px;
        height: 70px;
        margin:10px;
        padding: 20px;
        border-radius: 10px;
    }
    h3{
        color:indigo;
        width:120px;
        cursor: pointer;
    }
</style>