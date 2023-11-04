<template lang="pug">
doctype html
.m-4(v-auto-animate)
  .text-4xl Todos
  div
    TodoStatusSelector.mt-2(v-model="page")
    TodoList.mt-2(:filter="filterFuncs[page]", v-model="todos")
  .text-4xl.mt-4 Add
  TodoEdit.mt-2(v-model="newTodo", @save="saveNewTodo", :key="newTodo.key")
</template>

<script setup lang="ts">
const todos = reactive(JSON.parse(localStorage.getItem("todos") || "[]"));
watchEffect(() => localStorage.setItem("todos", JSON.stringify(todos)));

const page = ref<"all" | "open" | "closed">("open");
const filterFuncs = {
  all: () => true,
  open: (todo: TodoItem) => todo.open,
  closed: (todo: TodoItem) => !todo.open,
};

const genNewTodo = () => ({
  title: "",
  description: "",
  open: true,
  key: Math.random(),
});

const newTodo = ref(genNewTodo());

const saveNewTodo = () => {
  todos.push(newTodo.value);
  newTodo.value = genNewTodo();
};
</script>
