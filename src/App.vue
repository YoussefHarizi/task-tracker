<template>


    <div class="container">
      <Header title="Task Tracker" @clicked-btn="showtask=!showtask"/>
      <AddTask @add-task="addTask" v-show="showtask"/>
      <Tasks @task-done="taskDone" @delete-task="deleteTask" :tasks="tasks"/>
    </div>
  

  
</template>
<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'
export default {
  name:'App',
  components:{
    Header,
    Tasks,
    AddTask

  },
  data(){
    return {
      showtask:false,
      tasks:[]
    }
  },
  methods:{
    addTask(task){
      this.tasks=[...this.tasks,task]
    },
    deleteTask(id){
      if(confirm('Are you sure to delete this task?')){

        this.tasks=this.tasks.filter((task)=>task.id!==id)
      }
    },
    taskDone(id){
      this.tasks=this.tasks.map((task)=>task.id==id?{...task,remender:!task.remender}:task)

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

