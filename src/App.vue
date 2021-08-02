<template>
 <div class='container'>
  <Header @show-addTask="toggleShowAddTask" 
  :showAddTask="showAddTask"
   title='Task Tracker' />
  <AddTask v-show="showAddTask" @addTask=" addTask " />
<TaskList @toggleReminder="toggleReminder" @deleteTask="deleteTask" :tasks="tasks" />

 </div>
</template>

<script>
import Header from './components/Header.vue'
import TaskList from "./components/TaskList.vue"
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    TaskList,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask : false
    }
  },
  methods: {
    deleteTask(task) {
      console.log(task.text);
      if (confirm (`Delete (${task.text}) ?`)) {
        this.tasks = this.tasks.filter((el) => el.id !== task.id )
      }
    },

    toggleReminder(id){
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder } : task )
    },
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    toggleShowAddTask() {
      this.showAddTask = !this.showAddTask
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doctor Appointment",
        day: "march 1st at 2:30",
        reminder: true
      },
       {
        id: 2,
        text: "Job interview",
        day: "march 8th at 2:30",
        reminder: false
       },
        {
        id: 3,
        text: "Lunch date with the misses",
        day: "march 4th at 2:30",
        reminder: true
        }
    ]
  }
}
</script>

<style >
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}


</style>
