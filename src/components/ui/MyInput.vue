<template>
  <input :value="modelValue" @input="updateInput" class="input" type="text" />
</template>

<script setup>

defineProps({
  modelValue: [String, Number],
});

const emit = defineEmits(['update:modelValue']);

const updateInput = (event) => {
  emit('update:modelValue', event.target.value);
};
</script>

<style scoped>
.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
}
</style>
