<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="header__title display-2 font-weight-bold mb-3">Todo List</h1>
        <v-text-field label="new todo" solo v-model="newTodo"></v-text-field>
        <v-btn elevation="2" @click="addTodo">Add Todo</v-btn>
        <div v-if="todoList.length > 0">
          <div v-for="todoItem in todoList" :key="todoItem.id">
            <v-checkbox
              v-model="todoItem.isCompleted"
              color="red"
              hide-details
            ></v-checkbox>
            <v-text-field
              v-if="todoItem.isEdit"
              solo
              v-model="todoItem.todo"
            ></v-text-field>
            <label
              v-else
              :class="{ 'text-decoration-line-through': todoItem.isCompleted }"
              >{{ todoItem.todo }}</label
            >
            <v-icon
              class="pointer"
              v-if="todoItem.isEdit"
              @click="editTodo(todoItem.id)"
            >
              mdi-content-save-outline
            </v-icon>
            <v-icon class="pointer" v-else @click="editTodo(todoItem.id)">
              mdi-pencil-outline
            </v-icon>
            <v-icon class="pointer" @click="deleteTodo(todoItem.id)">
              mdi-delete
            </v-icon>
          </div>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "HelloWorld",
  methods: {
    addTodo() {
      this.todoList.push({
        id: uuidv4(),
        isCompleted: false,
        isEdit: false,
        todo: this.newTodo,
      });
      console.log(this.todoList);
      this.newTodo = "";
    },
    deleteTodo(id) {
      this.todoList = this.todoList.filter((todoItem) => todoItem.id !== id);
    },
    editTodo(id) {
      console.log("edit");
      this.todoList = this.todoList.map((todoItem) =>
        todoItem.id === id
          ? { ...todoItem, isEdit: !todoItem.isEdit }
          : todoItem
      );
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
.pointer {
  cursor: pointer;
}
</style>
