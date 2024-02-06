<!-- src/App.vue -->
<template>
  <div id="app" class="p-8 bg-orange-400">
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  components: {
    TodoList,
  },
};
</script>


