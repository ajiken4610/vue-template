<template lang="pug">
.border.rounded.p-4(v-if="!editing")
  .float-right
    button.border.rounded.mx-1.px-2(@click="editing = true") Edit
    button.border.rounded.mx-1.px-2(@click="emit('delete')") Delete
  .text-2xl {{ todo?.title }}
  .whitespace-pre-wrap {{ todo?.description }}
  div: label
    input.mx-2.inline-block(type="checkbox", v-model="closed")
    .inline(v-auto-animate)
      .inline-block(v-if="todo?.open") Open
      .inline-block(v-else) Closed
TodoEdit(v-else-if="todo", v-model="todo", @save="editing = false")
</template>

<script setup lang="ts">
const props = defineProps<{ modelValue: TodoItem | undefined }>();
const emit = defineEmits<{
  "update:modelValue": [todo: TodoItem];
  delete: [];
}>();

const todo = computed({
  get: () => (props.modelValue && reactive(props.modelValue)) || null,
  set: (todo) => todo && emit("update:modelValue", todo),
});
const closed = computed({
  get: () => todo.value && !todo.value.open,
  set: (closed) => todo.value && (todo.value.open = !closed),
});
const editing = ref(false);
</script>
