<template>
  <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
    <!-- binding a class on the condition that the parameter is true can be added even if a class was already assigned-->
    <p>
      <input type="checkbox" v-on:change="markComplete" />
      <!-- v-on directive is used to check events v-on:click, v-on:submit-->
      {{todo.title}}
      <button @click="$emit('del-todo',todo.id)" class="del">x</button>
      <!-- @click can also be made with the v-on:click. After $emit, It's being named and passing one parameter -->
      <!-- this parameter is sent as a payload -->
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>