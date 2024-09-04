<script setup>
import { reactive } from 'vue';
// importando os compenetes
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estuda Vue',
        finalizada: false,
      },
      {
        titulo: 'Estuda SASS',
        finalizada: true,
      },
      {
        titulo: 'Estuda Gulp',
        finalizada: true
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  };

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  };

  const getTarefasFiltradas = () => {
    // e a mesma coisa de const filtro = estado.filtro
    const {filtro} = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  };

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  };
</script>

<template>
  <div class="container">
    <!-- Utilizando os compenentes -->
    <!-- 
      em Cabecalho -  tarefas-pendentes é uma funcao criada dentro do compenente,
      onde podemos passar a funcao getTarefasPendentes que esta no App.vue
     -->
     <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
     <Formulario :troca-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-tempo="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
     <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>


