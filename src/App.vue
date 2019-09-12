<template>
  <div>
  <h2>To-Do List</h2>
    <md-card class="cardBox">
      <section>
        <div class="todoBox">
          <li v-for="(todo, index) in todos" :key="todo.id">
            <md-checkbox v-model='todo.completed' class="md-primary"></md-checkbox>

                  <span
                    class="todo-item-label"
                    :class='{completed: todo.completed}'
                    @dblclick='editTodo(todo)'
                    v-if="!todo.edit">
                      {{ todo.label }}
                  </span>
                    <md-input v-else class="todo-item-edit" type="text" v-model='todo.label' @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.escape="doneEdit(todo)">
                    </md-input>
              <md-button class="md-accent" @click="removeTodo(index)">Delete</md-button>
          </li>
      </div>
      <md-field>
        <md-input v-model="currentTodo" @keydown.enter="addTodo(todo)" placeholder="Add a todo"></md-input>
      </md-field>
    </section>
    </md-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
    todos: [
      {
        'id': 1,
        'label': 'pay bills',
        'completed': false,
        'edit': false
      },
        {
        'id': 2,
        'label': 'go jogging',
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
      if (this.currentTodo.trim() == 0) {
            return
      }
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false, edit: false});
      this.currentTodo = '';
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.edit = true
    },
    doneEdit(todo) {
      todo.edit = false
    }
  }
};
</script>

<style>

#app {
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
  }

li {
  list-style: none;
  }

.container {
  width: 50%;
  margin: auto;
  text-align: center;
}

h2{
  text-align: center;
}

.completed {
  text-decoration: line-through;
}

.todoBox {
  font-size: 1.5em;
}
.cardBox {
  padding: 90px;
}
</style>
