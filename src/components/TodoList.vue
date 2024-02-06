<!-- src/components/TodoList.vue -->
<template>
  <div class = "flex flex-col min-h-screen min-w-full  items-center p-10">
    <h2 class="text-3xl font-bold mb-4 text-center p-8">Todo List</h2>
    <div class="flex mb-4 justify-center">
      <input v-model="newTodo" class="border p-2 mr-2" />
      <button @click="addTodo" class="bg-blue-500 text-white px-4 py-2">Add Todo</button>
    </div>
    <select v-model="filter" @change="filterTodo" class="border p-2 mb-4 flex justify-center" defaultValue="all">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="uncompleted">Uncompleted</option>
    </select>
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id" :class="{ completed: todo.completed }" class="flex items-center mb-2">
        <span class="mr-2">{{ todo.text }}</span>
        <button @click="toggleComplete(todo.id)" class="mr-2">{{ todo.completed ? 'Undo' : 'Complete' }}</button>
        <button @click="deleteCheck(todo.id)" class="text-red-500">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
      filter: 'all',
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        const todo = {
          id: Date.now(),
          text: this.newTodo,
          completed: false,
        };

        this.todos.push(todo);
        this.newTodo = '';
      }
    },
    deleteCheck(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    toggleComplete(id) {
      this.todos = this.todos.map(todo =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      );
    },
    filterTodo() {
      // Handle filtering logic here
    },
  },
  computed: {
    filteredTodos() {
      switch (this.filter) {
        case 'all':
          return this.todos;
        case 'completed':
          return this.todos.filter(todo => todo.completed);
        case 'uncompleted':
          return this.todos.filter(todo => !todo.completed);
        default:
          return this.todos;
      }
    },
  },
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
