<template>
  <header>
    <h1>{{ title }}</h1>
    <Button  v-if="homePage"
    @toggleAddTask="$emit('show-addTask')"  :color=" showAddTask ? 'red' : 'green' " :text="showAddTask ? 'Close' : 'Add Task' " />
  </header>
    <i> double click on a task to toggle reminder </i>

</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  props: {
    title: String,
    showAddTask: Boolean
  },
  components: {
    Button,
  },
  computed: {
    homePage() {
      if (this.$route.path === '/') {
        return true
      } else {
        return false
      }
    }
  }
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
i {
  font-size: 12px;
}
</style>
