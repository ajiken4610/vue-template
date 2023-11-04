<template lang="pug">
div(v-auto-animate)
  template(v-if="todos.filter(filter).length")
    template(v-for="(todo, i) of todos", :key="todo.key")
      TodoItem.my-2(
        v-if="filter(todo)",
        v-model="todos[i]",
        @delete="todos.splice(i, 1)"
      )
  div(v-else, key="notodos") No todos
</template>

<script setup lang="ts">
const props = defineProps<{
  filter: (todo: TodoItem) => boolean;
  modelValue: TodoItem[];
}>();
const emit = defineEmits<{ "update:modelValue": [todos: TodoItem[]] }>();

const todos = computed({
  get: () => reactive(props.modelValue),
  set: (todos) => emit("update:modelValue", todos),
});
</script>
