<template>
  <div class="bg-yellow-400 p-4">
    <h1
      class="text-3xl font-bold text-white text-center uppercase tracking-widest"
    >
      Simple Vue Todo App
    </h1>
  </div>

  <section class="w-2/2 sm:w-1/2 lg:w-1/3 sm:m-auto m-10 sm:my-10">
    <form
      class="flex gap-1 mb-5"
      @submit.prevent="editId ? updateTodo() : handleSubmit()"
    >
      <input
        type="text"
        class="form-input flex-1 rounded-lg border-yellow-300 focus:ring-yellow-500 focus:border-yellow-500"
        placeholder="Write new todo..."
        v-model="todo"
      />
      <button
        type="submit"
        class="rounded-lg text-white px-7 uppercase font-bold"
        :class="editId ? 'bg-yellow-500' : 'bg-yellow-400 '"
      >
        {{ editId ? "Edit" : "Add" }}
      </button>

      <button
        class="rounded-lg text-white px-7 uppercase font-bold bg-red-600"
        v-if="editId"
        @click="
          editId = null;
          todo = '';
        "
      >
        Cancel
      </button>
    </form>

    <Todo
      v-for="todo in todoList"
      :todo="todo"
      :key="todo.id"
      @delete="deleteTodo"
      @update="editTodo"
    />
  </section>
</template>

<script>
import Todo from "./components/Todo.vue";

export default {
  components: { Todo },
  data() {
    return {
      todo: "",
      todoList: localStorage.getItem("todos")
        ? JSON.parse(localStorage.getItem("todos"))
        : [],
      editId: null,
    };
  },
  methods: {
    handleSubmit() {
      const newTodo = { id: Date.now().toString(), title: this.todo };
      this.todoList.push(newTodo);
      localStorage.setItem("todos", JSON.stringify(this.todoList));
      this.todo = "";
    },

    deleteTodo(id) {
      this.todoList = this.todoList.filter((item) => item.id !== id);
      localStorage.setItem("todos", JSON.stringify(this.todoList));
    },

    editTodo(todo) {
      this.editId = todo.id;
      this.todo = todo.title;
    },

    updateTodo() {
      this.todoList = this.todoList.map((item) =>
        item.id === this.editId ? { ...item, title: this.todo } : item
      );
      localStorage.setItem("todos", JSON.stringify(this.todoList));

      this.todo = "";
      this.editId = null;
    },
  },
};
</script>
