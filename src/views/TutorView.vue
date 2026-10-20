<!-- Endpoint:  Listar tutores
Método:  GET
Ação:  /tutores

Endpoint:  Visualizar tutor por iD
Método:  GET
Ação:  /tutores

Endpoint: Remover tutor  por iD
Método: DELETE
Ação: /tutores/{id} -->

<script setup>
import { onMounted, ref } from 'vue';

const API_URL = 'http://localhost:3000';
const tutores = ref([]);

async function carregarDados() {
  const respostaTutores = await fetch(`${API_URL}/tutores`);
  tutores.value = await respostaTutores.json();
}

async function excluirTutor(id) {
  const confirmarExclusao = window.confirm(
    'Tem certeza que deseja excluir esse tutor?',
  );
  if (confirmarExclusao) {
    await fetch(`${API_URL}/tutores/${id}`, {
      method: 'DELETE',
    });
    await carregarDados();
  }
}
onMounted(carregarDados);

//FIM DO SCRIPT
</script>

<template>
  <!--INICIO DO TEMPLATE-->
  <div>
    <header class="mb-4">
      <h1 class="text-2xl font-bold">Listagem de Tutores</h1>
      <p class="text-body-secondary mb-0">
        Listagem dos Tutores cadastrados no sistema.
      </p>
    </header>

    <table class="table table-striped table-hover">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nome</th>
          <th>CPF/CnPJ</th>
          <th>Telefone</th>
          <th>Email</th>
          <th>Pets(Qtd)</th>
          <th>Pets(Nomes)</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="tutor in tutores"
          :key="tutor.id"
        >
          <td>{{ tutor.id }}</td>
          <td>{{ tutor.nome }}</td>
          <td>{{ tutor.cpfCnpj }}</td>
          <td>{{ tutor.telefone }}</td>
          <td>{{ tutor.email }}</td>
          <td>{{ tutor.petsQtd }}</td>
          <td>{{ tutor.petsNomes }}</td>
          <td>




            <button
              class="btn btn-danger"
              @click="excluirTutor(tutor.id)"
            >
              EXCLUIR
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
