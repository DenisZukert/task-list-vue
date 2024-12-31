<template>
  <div class="todolist">
    <input
      type="text"
      v-model="title"
      placeholder="Add task"
      @keypress.enter="addTask"
    />
    <button
      @click="addTask"
      class="add-button"
    >
      Add
    </button>
    <div class="todo-container">
      <Todo
        v-for="task in tasks"
        :key="task.id"
        :id="task.id"
        :title="task.title"
        @remove="removeTask"
      />
    </div>
  </div>
</template>

<script setup>
import Todo from './Task.vue';
import { ref } from 'vue';

const tasks = ref([]);
const title = ref('');

const addTask = () => {
  if (title.value !== '') {
    tasks.value.push({ id: Date.now(), title: title.value.trim() });
    title.value = '';
  }
};

const removeTask = (id) => {
  tasks.value = tasks.value.filter((task) => task.id !== id);
};
</script>

<style scoped>
.todolist {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 5px;
  max-width: 1080px;
  width: 50%;
  left: 50%;
  transform: translate(-50%);
  padding: 5px;
}

.add-button {
  width: 30%;
  align-self: center;
}

.todo-container {
  display: flex;
  background-color: coral;
  flex-direction: column;
  gap: 5px;
}
</style>
