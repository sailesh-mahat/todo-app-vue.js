<template>
  <div>
    <input v-model="currentTodo" @keydown.enter="addTodo(todo)" placeholder="Add a todo">
    <ul class="todos">
      <li v-for="(todo, index) in todos" :key="todo.id">
        <input type='checkbox' v-model='todo.completed' >
            <div>
              <span
                class="todo-item-label"
                :class='{completed: todo.completed}'
                @dblclick='editTodo(todo)'
                v-if="!todo.edit">
                  {{ todo.label }}
              </span>
                <input v-else class="todo-item-edit" type="text" v-model='todo.label'>
              </div>
          <button @click="removeTodo(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  data() {
    return {
    todos: [
    {
      'id': 1,
      'label': 'trash',
      'completed': false,
      'edit': false
    },
      {
      'id': 2,
      'label': 'dishes',
      'completed': false,
      'edit': false
    },
  ],
    currentTodo: '',
    editedTodo: null
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false, edit: false});
      this.currentTodo = '';
    }
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
      },
    editTodo(todo) {
      todo.edit = true
    }
  }
};

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.completed {
  text-decoration: line-through;
}
</style>
