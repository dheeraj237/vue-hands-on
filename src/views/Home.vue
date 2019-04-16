<template>
  <div id="app">
    <!-- {{msg}} -->
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <Header/> -->
    <AddTodo v-on:add-todo="addTodo"/>
    <ToDos v-bind:todos="todos" v-on:del-todo="delToDo"></ToDos>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import Header from "../components/layouts/Header.vue";
import ToDos from "../components/ToDos.vue";
import AddTodo from "../components/AddTodo.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    // HelloWorld
    // Header,
    ToDos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    delToDo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => (this.todos = this.todos.filter(todo => todo.id !== id)))
        .catch(err => console.err(err));
      // this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newToDo) {
      const { title, completed } = newToDo;

      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(res => (this.todos = [...this.todos, res.data]))
        .catch(err => console.err(err));

      // this.todos = [...this.todos, newToDo];
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(res => (this.todos = res.data))
      .catch(err => console.err(err));
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
