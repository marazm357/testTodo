<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script setup>
</script>

<style scoped>
.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}
</style>
