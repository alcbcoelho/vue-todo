<script setup>
const props = defineProps(["tasks"])
</script>

<template>
    <div class="alert alert-light mt-4 text-center" v-if="!props.tasks.length">Não há tarefas para serem exibidas.</div>
    <ul v-else class="list-group mt-4">
      <li v-for="task in props.tasks" class="list-group-item">
        <input @change="(e) => task.done = e.target.checked" :id="task.name" type="checkbox" :checked="task.done">
        <label :class="{ done: task.done }" class="ms-2" :for="task.name">
          {{ task.name }}
        </label>
      </li>
    </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>