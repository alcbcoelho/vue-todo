<script setup>
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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getPendingTasks().length }} tarefas pendentes
      </p>
    </header>
    <!-- @{event-name}.prevent: invokes e.preventDefault() -->
    <form @submit.prevent="registerTask">
      <div class="row">
        <div class="col">
          <input required @change="(e) => state.newTaskName = e.target.value" class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa" :value="state.newTaskName">
        </div>
        <div class="col-md-1">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="(e) => state.filter = e.target.value"  class="form-control">
            <option value="all">Todas as tarefas</option>
            <option value="pending">Tarefas pendentes</option>
            <option value="done">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li v-for="task in getFilteredTasks()" class="list-group-item">
        <input @change="(e) => task.done = e.target.checked" :id="task.name" type="checkbox" :checked="task.done">
        <label :class="{ done: task.done }" class="ms-2" :for="task.name">
          {{ task.name }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
