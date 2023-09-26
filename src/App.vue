<script setup>
import { reactive } from "vue";
import Header1 from "./components/Header1.vue";
import Form from "./components/Form.vue";
import TaskList from "./components/TaskList.vue";

const estado = reactive({
  tarefaTemp: "",

  filtro: "todas",

  tarefas: [],
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
    <Header1 :tarefas-pendentes="getTarefasPendentes().length" />

    <Form
      :tarefa-temp="estado.tarefaTemp"
      :edita-tarefa-temp="(e) => (estado.tarefaTemp = e.target.value)"
      :cadastrar-tarefa="cadastrarTarefa"
      :trocar-filtro="(e) => (estado.filtro = e.target.value)"
    />

    <TaskList :tarefas="getTarefasFiltradas()"></TaskList>
  </div>
</template>
