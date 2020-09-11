<template>
  <div id="app">
    <Header />
    <!-- Components are embedded, props can be passed-->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    <!-- Directive v-bind: pass the data as props to the component-->
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todos from "./components/Todos";

export default {
  name: "app",
  components: { Header, Todos },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Todo one",
          completed: false,
        },
        {
          id: 2,
          title: "Todo two",
          completed: true,
        },
        {
          id: 3,
          title: "Todo three",
          completed: false,
        },
      ],
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  },
};
</script>


<style>
/* Style is global */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
