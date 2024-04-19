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
      <tbody>
        <TodoTask v-for="todo in todos" :item="todo" :key="todo.id" />
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
import TodoTask from '@/components/TodoTask.vue';
import TodoList from '@/components/TodoList.vue';

export default {
  name: 'TodoView',
  components: {
    TodoTask,
    TodoList
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
    axios.get('https://jsonplaceholder.typicode.com/todos')
      .then(response => {
        // en cas de réussite de la requête
        this.todos = response.data;
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
