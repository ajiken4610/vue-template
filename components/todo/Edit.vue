<template lang="pug">
.border.rounded.p-4
  .text-xl Title
  input.border.rounded.w-full(v-model="copy.title")
  div(v-auto-animate)
    .text-sm(v-if="showValidator") (!) Required.
  .text-xl.mt-4 Description
  textarea.border.rounded.w-full(v-model="copy.description")
  .mt-4: button.border.rounded.px-2(@click="save") Save
</template>

<script setup lang="ts">
const props = defineProps<{ modelValue: TodoItem }>();
const emit = defineEmits<{ "update:modelValue": [todo: TodoItem]; save: [] }>();

const todo = computed({
  get: () => reactive(props.modelValue),
  set: (todo) => emit("update:modelValue", todo),
});

const copy = ref();
watchEffect(() => (copy.value = JSON.parse(JSON.stringify(todo.value))));

const showValidator = ref(false);

const save = () => {
  if (copy.value.title) {
    todo.value = copy.value;
    emit("save");
    showValidator.value = false;
  } else {
    showValidator.value = true;
  }
};
</script>
