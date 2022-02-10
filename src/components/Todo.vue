<template>
  <div
    class="bg-white w-auto p-3 my-3 rounded-xl shadow-sm shadow-slate-300 flex items-center justify-between relative overflow-hidden"
    @click="$emit('complete', todo)"
  >
    <div
      class="bg-yellow-300 w-1.5 h-full absolute top-0 left-0"
      :class="{ 'bg-green-400': todo.complete }"
    />

    <div class="ml-2">
      <h2 class="text-lg font-medium">{{ todo.title }}</h2>
      <p class="text-xs font-medium text-gray-400">
        Created At {{ todoCreatedTime }}
      </p>
    </div>

    <div class="flex items-center gap-4">
      <p
        class="text-sm hover:cursor-pointer"
        @click.stop="$emit('update', todo)"
      >
        &#9998;
      </p>

      <p
        class="text-2xl font-bold text-red-600 hover:cursor-pointer"
        @click.stop="$emit('delete', todo.id)"
      >
        &times;
      </p>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  props: {
    todo: { type: Object, required: true },
  },

  data() {
    return {
      todoCreatedTime: moment(this.todo.createdAt).startOf("minutes").fromNow(),
    };
  },

  methods: {
    createdTime() {
      this.todoCreatedTime = moment(this.todo.createdAt)
        .startOf("minutes")
        .fromNow();
    },
  },

  mounted() {
    setInterval(this.createdTime, 1000 * 60);
  },
};
</script>
