<template>
  <div
    class="bg-white w-auto p-3 my-3 rounded-xl shadow-sm shadow-slate-300 flex items-center justify-between"
  >
    <h2 class="text-lg font-medium">{{ todo.title }}</h2>

    <div class="flex items-center gap-4">
      <p class="text-sm hover:cursor-pointer" @click="$emit('update', todo)">
        &#9998;
      </p>

      <p
        class="text-2xl font-bold text-red-600 hover:cursor-pointer"
        @click="$emit('delete', todo.id)"
      >
        &times;
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todo: { type: Object, required: true },
  },
};
</script>
