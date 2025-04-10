<template>
  <div v-for="task in props.tasks" :key="task.id">
    <label class="check">
      <div class="checkInput">
        <input type="checkbox" :checked="task.completed" @change="$emit('toggle-complete', task.id)" />
      </div>
      <MyInput type="text" :value="task.title" @input="updateTitle($event, task.id)" />
      <MyBtn @click="$emit('delete-task', task.id)">Удалить</MyBtn>
    </label>
  </div>
</template>

<script setup>
import MyInput from '@/components/ui/MyInput.vue';
import MyBtn from '@/components/ui/MyBtn.vue'

const emit = defineEmits(['edit-task', 'delete-task'])

const props = defineProps({
  tasks: Array,
});


const updateTitle = (event, taskId) => {
  emit('edit-task', taskId, event.target.value);
};
</script>

<style scoped>
.check {
  display: flex;
  flex-direction: row;
  justify-content: left;
}

.checkInput {
  display: flex;
  border: 1px solid teal;
  padding: 8px;
  justify-content: center;
  align-content: center;
}
</style>
