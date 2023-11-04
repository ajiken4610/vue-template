<template lang="pug">
div
  label
    input.mx-2(type="radio", value="all", v-model="selected")
    | All
  label
    input.mx-2(type="radio", value="open", v-model="selected")
    | Open
  label
    input.mx-2(type="radio", value="closed", v-model="selected")
    | Closed
</template>

<script setup lang="ts">
import { computed } from "vue";
const props = defineProps<{ modelValue: "all" | "open" | "closed" }>();
const emit = defineEmits<{
  "update:modelValue": [selected: "all" | "open" | "closed"];
}>();

const selected = computed({
  get: () => props.modelValue,
  set: (selected) => emit("update:modelValue", selected),
});
</script>
