<template>
  <div id="app">
    <TaskManager />
  </div>
</template>

<script>
import TaskManager from './components/TaskManager.vue';

export default {
  name: 'App',
  components: {
    TaskManager
  }
};
</script>

<style>
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #e0f7fa;
}
</style>