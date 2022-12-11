<template>


    <div class="container">
      <Header title="Task Tracker"/>
      <Tasks @delete-task="deleteTask" :tasks="tasks"/>
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
  methods:{
    deleteTask(id){
      if(confirm('Are you sure to delete this task?')){

        this.tasks=this.tasks.filter((task)=>task.id!==id)
      }
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

