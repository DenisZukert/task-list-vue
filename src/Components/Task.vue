<template>
  <div
    class="todo"
    @dblclick="editMode = true"
  >
    <input
      type="checkbox"
      v-model="task.isChecked"
    />
    <div v-if="!editMode">{{ task.title }}</div>
    <input
      v-else
      type="text"
      v-model="task.title"
      @blur="editMode = false"
      @keypress.enter="editMode = false"
      @keydown.esc="cancelEdit"
    />
    <button @click="removeTask">X</button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits, ref } from 'vue';

const props = defineProps({
  id: Number,
  title: String,
});

const emit = defineEmits(['remove']);

const task = ref({
  id: props.id,
  title: props.title,
  isChecked: false,
});

const editMode = ref(false);

const removeTask = () => {
  emit('remove', task.value.id);
};

const cancelEdit = () => {
  editMode.value = false;
  task.value.title = props.title;
};
</script>

<style scoped>
.todo {
  display: flex;
  border: 1px solid black;
  justify-content: space-between;
  padding: 8px;
  align-items: center;
}

button {
  background-color: red;
  color: white;
  border: none;
  padding: 4px 8px;
  cursor: pointer;
}

button:hover {
  background-color: darkred;
}
</style>
