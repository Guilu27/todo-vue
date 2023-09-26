<script setup>
const props = defineProps(["tarefas"]);
</script>

<template>
  <ul v-if="props.tarefas.length > 0 > 0" class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input
        @change="(e) => (tarefa.finalizado = e.target.checked)"
        :checked="tarefa.finalizado"
        :id="tarefa.titulo"
        type="checkbox"
      />
      <label
        :class="{ done: tarefa.finalizado }"
        class="ms-3"
        :for="tarefa.titulo"
      >
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
  <p class="text-center mt-3" v-else>Nao possui nem uma tarefa</p>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
