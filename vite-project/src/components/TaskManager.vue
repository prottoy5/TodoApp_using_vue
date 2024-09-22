<template>
  <div class="app">
    <h1>{{ title }}</h1>

    <input
      type="text"
      v-model="newTask"
      @keyup.enter="addTask"
      placeholder="Add a new task"
    />
    <button @click="addTask">Add Task</button>

    <h2>Tasks</h2>

    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task">
        <span :class="{ completed: task.completed }">{{ task.name }}</span>
        <span>{{ task.completed ? 'Done' : 'Pending' }}</span>
        <div class='btns'>
          <button class='complete' @click="toggleTaskCompletion(task)">Complete</button>
          <button class='delete' @click="removeTask(task, index)">Delete</button>
        </div>
      </li>
    </ul>

    <p v-if="tasks.length === 0">No tasks available.</p>

    <h3>Task Status: {{ taskStatus }}</h3>
    <p>Total Tasks: {{ tasks.length }}</p>
    <p>Completed Tasks: {{ completedTasks.length }}</p>
    <p>Incomplete Tasks: {{ incompleteTasks.length }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Vue Task Manager',
      newTask: '',
      tasks: [
        { name: 'Learn Vue.js', completed: false },
        { name: 'Learn Laravel', completed: false }
      ]
    };
  },
  computed: {
    completedTasks() {
      return this.tasks.filter(task => task.completed);
    },
    incompleteTasks() {
      return this.tasks.filter(task => !task.completed);
    },
    taskStatus() {
      return this.completedTasks.length === this.tasks.length && this.tasks.length > 0
        ? 'All tasks completed!'
        : 'There are tasks to complete.';
    }
  },
  methods: {
    addTask() {
      const taskName = this.newTask.trim();
      if (taskName) {
        this.tasks.push({ name: taskName, completed: false });
        this.newTask = '';
      } else {
        alert('Task name cannot be empty!');
      }
    },
    removeTask(task, index) {
      if (task.completed) {
        this.tasks.splice(index, 1);
      } else {
        alert('Complete the task before deleting!');
      }
    },
    toggleTaskCompletion(task) {
      task.completed = !task.completed;
    }
  }
};
</script>

<style scoped>
.app {
  max-width: 600px;
  margin: 50px auto;
  background: #fff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
  border: 1px solid #b3e5fc;
}

h1, h2 {
  color: #0288d1;
}

input[type="text"] {
  width: calc(100% - 100px);
  padding: 10px;
  border: 1px solid #0288d1;
  border-radius: 5px;
  margin-bottom: 10px;
  font-size: 16px;
  outline: none;
}

button {
  background-color: #0288d1;
  color: white;
  border: none;
  padding: 10px 15px;
  margin-left: 10px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  outline: none;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0277bd;
}

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #f1f8ff;
  border: 1px solid #b3e5fc;
  border-radius: 5px;
  margin-bottom: 10px;
  transition: background-color 0.3s ease;
}

.task:hover {
  background-color: #e1f5fe;
}

.completed {
  text-decoration: line-through;
  color: #228B22;
}

h3 {
  margin-top: 20px;
  color: #0288d1;
}

p {
  color: #555;
}

.complete {
  background-color: #228B22;
}

.delete {
  background-color: #EE4B2B;
}



</style>