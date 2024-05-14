<template>
  <div class="container">
    <h1>To-Do List</h1>
    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id">
        <span :class="{ completed: todo.completed }">{{ todo.title }}</span>
        <button @click="editTodo(todo)">Edit</button>
        <button @click="deleteTodo(todo)">Delete</button>
      </li>
    </ul>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" placeholder="Add new todo">
      <button type="submit">Add Todo</button>
    </form>
    <div v-if="editingTodo">
      <h2>Edit Todo</h2>
      <form @submit.prevent="updateTodo">
        <input type="text" v-model="editingTodo.title" placeholder="Edit todo">
        <button type="submit">Update</button>
        <button @click="cancelEdit">Cancel</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: '',
      editingTodo: null
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ title: this.newTodo, id: Date.now(), completed: false });
      this.newTodo = '';
    },
    editTodo(todo) {
      this.editingTodo = todo;
    },
    updateTodo() {
      const index = this.todos.findIndex(todo => todo.id === this.editingTodo.id);
      this.todos.splice(index, 1, this.editingTodo);
      this.editingTodo = null;
    },
    cancelEdit() {
      this.editingTodo = null;
    },
    deleteTodo(todo) {
      const index = this.todos.findIndex(t => t.id === todo.id);
      this.todos.splice(index, 1);
    }
  }
}
</script>

<style scoped>
  background-image {
  background-image: url('./assets/kucing.png'); 
  background-size: cover; /* Mengatur gambar agar menutupi seluruh area */
  background-position: center;
  }
.container {
  max-width: 400px;
  margin: 40px auto;
  padding: 20px;
  background-size: cover;
  background-position: center;
  border: 1px solid #ddd;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}     
.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-list li {
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.todo-list li:last-child {
  border-bottom: none;
}

.completed {
  text-decoration: line-through;
  color: #999;
}

button {
  background-color: #4CAF50;
  color: #fff;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}

button:hover {
  background-color: #3e8e41;
}

form {
  margin-top: 20px;
}

input[type="text"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
}

input[type="text"]:focus {
  border-color: #aaa;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>
