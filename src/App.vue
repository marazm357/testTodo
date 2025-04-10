<template>
  <div id="app">
    <h1 class="mainTitle">TODO List</h1>
    <AddTodoForm class="addForm" @add-task="addTask" />
    <TodoList :tasks="filteredTasks" @toggle-complete="toggleComplete" @edit-task="editTask"
      @delete-task="deleteTask" />
    <CompletedTasks :completed-tasks="completedTasks" />
    <div>
      <label>
        <MyBtn @click="changeShowComleted" v-model="showCompleted">Показать только выполненные задачи</MyBtn>
      </label>
    </div>
  </div>
</template>

<script setup>
import MyBtn from './components/ui/MyBtn.vue'

import { ref, computed, onMounted, watch } from 'vue';
import AddTodoForm from './components/AddTodoForm.vue';
import TodoList from './components/TodoList.vue';
import CompletedTasks from './components/CompletedTasks.vue';

const tasks = ref([]);
const showCompleted = ref(false);

const changeShowComleted = () => showCompleted.value = !showCompleted.value

const fetchTasks = async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/todos?_limit=10');
  const data = await response.json();
  tasks.value = data;
};

const addTask = (task) => {
  tasks.value.push(task);
};

const editTask = (taskId, updatedTitle) => {
  const task = tasks.value.find((task) => task.id === taskId);
  if (task) task.title = updatedTitle;
};

const toggleComplete = (taskId) => {
  const task = tasks.value.find((task) => task.id === taskId);
  if (task) task.completed = !task.completed;
};

const deleteTask = (taskId) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskId);
};

const completedTasks = computed(() => tasks.value.filter((task) => task.completed));
const filteredTasks = computed(() => (showCompleted.value ? completedTasks.value : tasks.value));

onMounted(() => {
  const storedTasks = localStorage.getItem('tasks');
  if (storedTasks) {
    tasks.value = JSON.parse(storedTasks);
  } else {
    fetchTasks();
  }
});

watch(
  tasks,
  (newTasks) => {
    localStorage.setItem('tasks', JSON.stringify(newTasks));
  },
  { deep: true }
);
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  margin: 10px;
  gap: 15px;
  justify-content: center;
}

.addForm {
  display: flex;
  justify-content: center;
}

.mainTitle {
  color: teal;
}
</style>
