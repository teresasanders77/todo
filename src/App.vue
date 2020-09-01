<template>
  <div class="container">
    <h1>To-Do List</h1>
    <md-card class="md-primary" md-with-hover>
      <md-ripple>
        <md-field>
          <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo"></md-input>
        </md-field>
      </md-ripple>
      <ul class="todos">
        <md-list v-for="todo in todos" :key="todo.id">
          <v-row class="row">
            <input class="checkboxButton" type="checkbox" v-model="todo.completed" />
            <span
              class="todo-item-label"
              :class="{completed: todo.completed}"
              @dblclick="editTodo(todo)"
              v-if="!todo.edit"
            >{{ todo.label }}</span>
            <md-input
              v-else
              class="todo-item-edit"
              type="text"
              v-model="todo.label"
              @blur="doneEdit(todo)"
              @keyup.enter="doneEdit(todo)"
              @keyup.escape="doneEdit(todo)"
            ></md-input>
            <button @click="removeTodo(todo)" class="x-btn">
              <x-icon size="1.5x" class="custom-class"></x-icon>
            </button>
          </v-row>
        </md-list>
      </ul>
    </md-card>
  </div>
</template>

<script>
import { XIcon } from "vue-feather-icons";

export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      editedTodo: null,
    };
  },
  components: {
    XIcon,
  },

  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        edit: false,
      });
      this.currentTodo = "";
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      todo.edit = true;
    },
    doneEdit(todo) {
      todo.edit = false;
    },
  },
};
</script>

<style>
.container {
  text-align: center;
  margin: 25px 400px 75px 400px;
  display: block;
}

@media only screen and (max-width: 600px) {
  .container {
    margin: auto;
    text-align: center;
  }
}
.completed {
  text-decoration: line-through;
  text-decoration-color: red;
}
.todo-item-label {
  font-size: 25px;
}
.checkboxButton {
  margin: 25px;
}
.todo-item-label {
  margin: 25px;
}
button {
  margin: 25px;
  background: none;
  color: red;
}
button:hover {
  cursor: pointer;
  color: #a50909;
}
.row {
  border-style: groove;
  text-align: left;
}
.todos {
  margin-right: 25px;
}
h1 {
  color: white;
}
</style>
