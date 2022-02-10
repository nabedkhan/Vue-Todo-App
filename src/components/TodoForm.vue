<template>
  <form class="flex gap-1 mb-5" @submit.prevent="$emit('handleSubmit')">
    <input
      type="text"
      class="form-input flex-1 rounded-lg border-yellow-300 focus:ring-yellow-500 focus:border-yellow-500"
      placeholder="Write new todo..."
      :value="modelValue"
      @change="$emit('update:modelValue', $event.target.value)"
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
      @click="$emit('handleCancel')"
    >
      Cancel
    </button>
  </form>
</template>

<script>
export default {
  props: {
    modelValue: { type: String, required: true },
    editId: { type: String, required: true },
  },
};
</script>
