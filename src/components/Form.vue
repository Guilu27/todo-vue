<script setup>
const props = defineProps([
  "cadastrarTarefa",
  "tarefaTemp",
  "trocarFiltro",
  "editaTarefaTemp",
]);
</script>

<template>
  <form @submit.prevent="props.cadastrarTarefa">
    <div class="row">
      <div class="col-md-9">
        <input
          type="text"
          placeholder="Digite aqui a descicao da tarefa"
          class="form-control"
          required
          @change="props.editaTarefaTemp"
          :value="props.tarefaTemp"
        />
      </div>
      <div class="col-md-1">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="props.trocarFiltro" class="form-control">
          <option value="todas">Todas as tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
