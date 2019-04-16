<template>
  <div>
    <!-- running fine -->
    <div v-for="todo in todos" :key="todo.id">
      <ToDoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"></ToDoItem>
      <!-- <h3>{{todo.title}}</h3> -->
    </div>
  </div>
</template>
<script>
import ToDoItem from "./ToDoItem.vue";

export default {
  name: "ToDos",
  components: {
    ToDoItem
  },
  props: ["todos"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
