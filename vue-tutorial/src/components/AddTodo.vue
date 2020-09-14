<template>
  <div>
    <form @submit="addTodo">
      <!-- Traverse upwards to the array
      Emit is not put here in order to first construct the Todo then send it-->
      <input
        type="text"
        v-model="title"
        name="title"
        placeholder="Add Todo..."
      />
      <!-- v-model bounds the value, so it can be accessed in js -->
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "AddTodo",
  data() {
    return { title: "" };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        id: uuidv4(),
        title: this.title,
        completed: false,
      };
      //Send up to parent by emitting an event
      this.$emit("add-todo", newTodo);
      //Clear the input
      this.title = "";
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}

input[type="text"] {
  flex: 10;
  padding: 5px;
}

input[type="submit"] {
  flex: 2;
}
</style>
