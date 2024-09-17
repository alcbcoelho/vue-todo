<script setup>
import Form from "./components/Form.vue";
import Header from "./components/Header.vue";
import List from "./components/List.vue";
import { reactive } from 'vue';

const state = reactive({
  filter: "all",
  tasks: [
    {
      name: "Estudar ES6",
      done: false,
    },
    {
      name: "Estudar SASS",
      done: false,
    },
    {
      name: "Ir para a academia",
      done: true,
    },
  ],
  newTaskName: "",
});

const getPendingTasks = () => state.tasks.filter(task => !task.done);
const getDoneTasks = () => state.tasks.filter(task => task.done);
const getFilteredTasks = () => {
  const { filter, tasks } = state;

  if (filter === "all")
    return tasks;
  return (filter === "done") ? getDoneTasks() : getPendingTasks();
}
const registerTask = () => {
  const { tasks, newTaskName  } = state;
  const newTask = {
    name: newTaskName,
    done: false,
  };

  tasks.push(newTask);
  newTaskName = "";
}
</script>

<template>
  <div class="container">
    <Header :pending-tasks="getPendingTasks().length" />
    <Form
      :new-task="state.newTaskName"
      :register-task="registerTask"
      :edit-new-task="(e) => state.newTaskName = e.target.value"
      :change-filter="(e) => state.filter = e.target.value"
    />
    <List :tasks="getFilteredTasks()" />
  </div>
</template>
