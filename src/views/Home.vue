<template>
  <AddTask v-show="showAddTask" @addTask="addTask" />
    <TaskList
      @toggleReminder="toggleReminder"
      @deleteTask="deleteTask"
      :tasks="tasks"
    />
</template>

<script>
import AddTask from "../components/AddTask.vue";
import TaskList from "../components/TaskList.vue";

export default {
    name: "Home",
    props: {
        showAddTask: Boolean,
    },
    components: {
        AddTask,
        TaskList,
    },
    data() {
        return {
            tasks: [],
        }
    },
    methods: {
   async deleteTask(task) {
      
      if (confirm(`Delete (${task.text}) ?`)) {
        const res = await fetch(`api/tasks/${task.id}`, {
          method: 'DELETE'
        })
        
        res.status === 200 ? (this.tasks = this.tasks.filter((el) => el.id !== task.id))
        : alert('Error deleting task')
      }
    },

    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const updtTask = { ...taskToToggle, reminder: !taskToToggle.reminder  }

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type' : 'application/json'
        },
        body: JSON.stringify(updtTask)
      })
      const data = await res.json()
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    async addTask(task) {
       const res = await fetch('api/tasks', {
         method: 'POST',
         headers: {
           'Content-type': 'application/json'
        },
        body: JSON.stringify(task)
       })

       const data = await res.json()

      this.tasks = [...this.tasks, data];
    },
    
    async fetchTasks() {
      const res = await fetch("api/tasks")
    const tasks = await res.json()
    this.tasks = tasks
    },

    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`)
    const task = await res.json()
    return task
    }
  },
  async created() {
    await this.fetchTasks();
  }
}
</script>

<style>

</style>