<template>
    <TodoList />
    <TodoTask />
</template>

<script>
import TodoList from '@/components/TodoList.vue';
import TodoTask from '@/components/TodoTask.vue';


export default {
  name: 'HomeView',
  components: {
    TodoList,
    TodoTask
  }
}
</script>
