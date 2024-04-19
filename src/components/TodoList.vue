<template>
    <div class="container">
        <div>{{ completedTasksCount }} / {{ todos.length }} tâches complétées</div>
        <div class="progress">
      <div class="progress-bar" role="progressbar" :style="{ width: completedPercentage + '%' }" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100">{{ completedPercentage }}%</div>
    </div>

    <table class="table">
  <thead>
    <tr>
      <th scope="col">A faire</th>
      <th scope="col">Fait</th>
    </tr>
  </thead>
  <tbody  v-for="item in todos" :key="item.id">
    <tr>
        <td><s v-if="item.completed">{{ item.title }}</s><span v-else>{{ item.title }}</span></td>
        <td><input type="checkbox" v-model="item.completed"</td>
    </tr>
  </tbody>
</table>
</div>
  </template>

<script>
import axios from 'axios';
import TodoList from '@/components/TodoList.vue';
import TodoTask from '@/components/TodoTask.vue';

export default {
  name: 'TodoView',
  components: {
    TodoList,
    TodoTask
  },
  data() {
    return {
      todos: [] // Initialisation de l'array des todos
    };
  },
  computed: {
    completedTasksCount() {
      return this.todos.filter(todo => todo.completed).length;
    },
    completedPercentage() {
      if (this.todos.length === 0) return 0; // Pour éviter une division par zéro
      return Math.round((this.completedTasksCount / this.todos.length) * 100);
    }
  },
  mounted() {
    let data = null;
    axios.get('https://jsonplaceholder.typicode.com/todos')
      .then(response => {
        // en cas de réussite de la requête
        console.log(response.data);
        this.todos = response.data;
      })
      .catch(error => {
        // en cas d’échec de la requête
        console.error(error);
      })
      .finally(() => {
        // dans tous les cas
      });
  }
}
</script>

<style>
.progress {
  height: 20px;
  margin-bottom: 20px;
}

.progress-bar {
  background-color: #007bff;
  color: #fff;
}
</style>