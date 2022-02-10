<template>
  <div class="flex gap-2 mb-2">
    <p
      class="font-medium text-sm text-blue-500 cursor-pointer"
      @click="$emit('changeFilter', '')"
    >
      All ({{ totalTodos }})
    </p>
    <p
      class="font-medium text-sm text-yellow-400 cursor-pointer"
      @click="$emit('changeFilter', 'incomplete')"
    >
      Incomplete ({{ inCompletedTodos }})
    </p>
    <p
      class="font-medium text-sm text-green-600 cursor-pointer"
      @click="$emit('changeFilter', 'complete')"
    >
      Complete ({{ completedTodos }})
    </p>
  </div>
</template>

<script>
export default {
  props: ["filteredValue", "todoList"],

  computed: {
    totalTodos() {
      return this.todoList.length;
    },

    completedTodos() {
      return this.todoList.filter((todo) => todo.complete).length;
    },

    inCompletedTodos() {
      return this.todoList.filter((todo) => !todo.complete).length;
    },
  },
};
</script>
