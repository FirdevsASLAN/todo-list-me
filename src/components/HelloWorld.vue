<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="header__title display-2 font-weight-bold mb-3">Todo List</h1>
        <v-text-field label="Solo" solo v-model="newTodo"></v-text-field>
        <v-btn elevation="2" @click="addTodo">Add Todo</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",
  methods: {
    addTodo() {
      this.todoList.push(this.newTodo);
      console.log(this.newTodo);
      this.newTodo = "";
    },
  },
  data() {
    return {
      newTodo: "",
      todoList: [],
    };
  },
};
</script>
<style lang="scss" scoped>
.header {
  &__title {
    margin-top: 5rem;
  }
}
</style>
