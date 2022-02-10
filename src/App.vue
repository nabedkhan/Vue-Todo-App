<template>
  <Heading />

  <section class="w-2/2 sm:w-1/2 lg:w-1/3 sm:m-auto m-10 sm:my-10">
    <TodoForm
      v-model="todo"
      @handleSubmit="handleSubmit"
      :editId="editId"
      @handleCancel="handleCancel"
    />

    <Filtered @changeFilter="handleChangeFilter" :todoList="todoList" />

    <Todo
      v-for="todo in filteredTodos"
      :todo="todo"
      :key="todo.id"
      @delete="deleteTodo"
      @update="editTodo"
      @complete="todoComplete"
    />
  </section>
</template>

<script>
import Filtered from "./components/Filtered.vue";
import Heading from "./components/Heading.vue";
import Todo from "./components/Todo.vue";
import TodoForm from "./components/TodoForm.vue";

export default {
  components: { Todo, TodoForm, Heading, Filtered },

  data() {
    return {
      todo: "",
      editId: "",
      todoList: [],
      filteredValue: "",
    };
  },

  methods: {
    handleSubmit() {
      if (this.editId) {
        this.todoList = this.todoList.map((item) =>
          item.id === this.editId ? { ...item, title: this.todo } : item
        );
        this.todo = "";
        this.editId = "";
      } else {
        const newTodo = {
          complete: false,
          title: this.todo,
          createdAt: new Date(),
          id: Date.now().toString(),
        };
        this.todoList.push(newTodo);
        this.todo = "";
      }
    },

    deleteTodo(id) {
      this.todoList = this.todoList.filter((item) => item.id !== id);
    },

    editTodo(todo) {
      this.editId = todo.id;
      this.todo = todo.title;
    },

    todoComplete(todo) {
      todo.complete = !todo.complete;
    },

    handleCancel() {
      this.editId = "";
      this.todo = "";
    },

    handleChangeFilter(value) {
      this.filteredValue = value;
    },
  },

  watch: {
    todoList: {
      handler(value) {
        localStorage.setItem("todoList", JSON.stringify(value));
      },
      deep: true,
    },
  },

  mounted() {
    this.todoList = JSON.parse(localStorage.getItem("todoList")) || [];
  },

  computed: {
    filteredTodos() {
      if (this.filteredValue === "incomplete") {
        return this.todoList.filter((item) => !item.complete);
      } else if (this.filteredValue === "complete") {
        return this.todoList.filter((item) => item.complete);
      } else {
        return this.todoList;
      }
    },
  },
};
</script>
