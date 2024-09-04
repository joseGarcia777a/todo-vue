<script setup>
  /*
    para a inportacao funcionar, e conseguir usar as informacoes geradas pelo getTarefasPendentes():
    1 - precisa ter no script a paralvar (setup) 
    2 - utilizamos uma variavel por padrao se chama (props)
    3 - e uma funcao do proprio vue (defineProps())
  */
  const props = defineProps(['tarefasPendentes']);
</script>
<template>
  <header class="p-5 mb-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        <!-- Você possui {{getTarefasPendentes().length}} tarefas pendentes -->
        <!-- o codigo e alterado para o de baixo props.tarefasPendentes -->
        Você possui {{props.tarefasPendentes}} tarefas pendentes
      </p>
    </header>
</template>