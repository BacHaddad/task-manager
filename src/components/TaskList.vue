<template>
  <div v-for="task in tasks" :key="task.id" >
      <Task @toggleReminder="$emit('toggleReminder', task.id)" @delete-task="deleteTask(task)" :task="task" />
  </div>
</template>

<script>
import Task from "./Task.vue"

export default {
name: "TaskList",
components: {
Task
},
props: {
    tasks: Array,
},
methods:{
    deleteTask(id) {
        this.$emit('deleteTask', id)
    }
},
emits: ['deleteTask', 'toggleReminder']
}
</script>

<style>

</style>