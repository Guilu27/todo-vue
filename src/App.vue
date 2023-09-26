<script setup>
import { reactive } from "vue";

const estado = reactive({
  tarefaTemp: "",

  filtro: "todas",

  tarefas: [
    {
      titulo: "estudar ES6",
      finalizado: false,
    },
    {
      titulo: "estudar SASS",
      finalizado: true,
    },
    {
      titulo: "Ir para a academia",
      finalizado: false,
    },
  ],
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter((tarefa) => !tarefa.finalizado);
};

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizado);
};

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();

    case "finalizadas":
      return getTarefasFinalizadas();

    default:
      return estado.tarefas;
  }
};

const cadastrarTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizado: false,
  };

  estado.tarefas.push(tarefaNova);

  estado.tarefaTemp = "";
};
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Voce possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>

    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col-md-9">
          <input
            type="text"
            placeholder="Digite aqui a descicao da tarefa"
            class="form-control"
            required
            @change="(e) => (estado.tarefaTemp = e.target.value)"
            :value="estado.tarefaTemp"
          />
        </div>
        <div class="col-md-1">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select
            @change="(e) => (estado.filtro = e.target.value)"
            class="form-control"
          >
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
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
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
