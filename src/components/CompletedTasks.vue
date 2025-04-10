<template>
  <div>
    <h2>Выполненные задачи</h2>
    <ul>
      <li v-for="task in completedTasks" :key="task.id">
        {{ task.title }}
      </li>
    </ul>
  </div>
</template>

<script setup>
defineProps({
  completedTasks: Array,
});
</script>
