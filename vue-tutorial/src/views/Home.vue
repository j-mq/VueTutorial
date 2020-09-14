<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <!-- v-on gets an emmitted event -->
    <!-- Components are embedded, props can be passed-->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    <!-- Directive v-bind: pass the data as props to the component-->
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: "Home",
  components: { Todos, AddTodo },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos${id}`)
        .then((this.todos = this.todos.filter((todo) => todo.id !== id)))
        .catch((error) => console.log(error));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios.post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed,
        })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((error) => console.log(error));
      //this.todos = [...this.todos, newTodo];
    },
  },
  created() {
    //Fires off when the component loads
    //With axios
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => (this.todos = res.data))
      .catch((error) => console.log(error));

    //Example with fetch API
    // const url = "https://jsonplaceholder.typicode.com/todos?_limit=5";
    // fetch(url)
    //   .then((res) => res.json())
    //   .then((res) => (this.todos = res))
    //   .catch(function(error) {
    //     console.log(error);
    //   });
  },
};
</script>
