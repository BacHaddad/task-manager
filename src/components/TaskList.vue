<template>
  <div v-for="task in tasks" :key="task.id" >
      <Task :task="task" />
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
    tasks: Array
}
}
</script>

<style>

</style>