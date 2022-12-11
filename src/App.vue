<template>


    <div class="container">
      <Header title="Task Tracker"/>
      <Tasks :tasks="tasks"/>
    </div>
  

  
</template>
<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
export default {
  name:'App',
  components:{
    Header,
    Tasks

  },
  data(){
    return {

      tasks:[]
    }
  },
  created(){
    this.tasks=[
      {
        id:1,
        text:'First Task',
        day:'March 1st at 2:30pm',
        remender:true,
      },
      {
        id:2,
        text:'second Task',
        day:'Juin 1st at 2:30pm',
        remender:false,
      },
      {
        id:3,
        text:'Therd Task',
        day:'March 1st at 2:30pm',
        remender:true,
      },
      ]
  }
}
</script>

