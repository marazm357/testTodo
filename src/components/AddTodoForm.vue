<template>
  <form @submit.prevent>
    <MyInput v-model="newTaskTitle" placeholder="Введите задачу" />
    <MyBtn @click="addTask">Добавить</MyBtn>
  </form>
</template>

<script setup>
import MyInput from '@/components/ui/MyInput.vue';
import MyBtn from '@/components/ui/MyBtn.vue'
import { ref } from 'vue';

const emit = defineEmits(['add-task'])

const newTaskTitle = ref('');


const addTask = () => {
  if (newTaskTitle.value.trim()) {
    const newTask = {
      id: Date.now(),
      title: newTaskTitle.value,
      completed: false,
    };
    emit('add-task', newTask);
    newTaskTitle.value = '';
  }
};
</script>
