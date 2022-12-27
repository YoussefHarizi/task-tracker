<template>


    <div class="container">
      <Header title="Task Tracker" @clicked-btn="toggleBtn" :closeadd="closeadd"/>
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
      tasks:[],
      closeadd:false,
    }
  },
  methods:{
    toggleBtn(){
      this.showtask=!this.showtask
      this.closeadd=!this.closeadd
      
    },
    async addTask(task){
      const res = await fetch('http://localhost:5000/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task),
      })
      const data = await res.json()

      this.tasks=[...this.tasks,data]
    },
    async deleteTask(id){
      if(confirm('Are you sure to delete this task?')){
        const res = await fetch(`http://localhost:5000/tasks/${id}`, {
          method: 'DELETE',
        })
        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert('Error deleting task')

      }
    },
    async taskDone(id){
      const taskToToggle = await this.fetchTask(id)
      const updTask = { ...taskToToggle, remender: !taskToToggle.remender }
      const res = await fetch(`http://localhost:5000/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updTask),
      })
      const data = await res.json()
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, remender: data.remender } : task
      )
    },

    async fetchTasks() {
      const res = await fetch('http://localhost:5000/tasks')
      const data = await res.json()
      return data
    },
    async fetchTask(id) {
      const res = await fetch(`http://localhost:5000/tasks/${id}`)
      const data = await res.json()
      return data
    },
  },
  
 
  async created(){
    this.tasks= await this.fetchTasks()
  }
}
</script>

