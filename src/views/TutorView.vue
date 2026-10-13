Endpoint:  Listar tutores
Método:  GET
Ação:  /tutores

Endpoint:  Visualizar tutor por iD
Método:  GET
Ação:  /tutores

Endpoint: Remover tutor  por iD
Método: DELETE
Ação: /tutores/{id}

<script setup>
import { onMounted, ref } from 'vue';

const API_URL = 'http://localhost:3000';

const pets = ref([]);
const tutores = ref([]);

async function carregarDados() {
  // const respostaPets = await fetch(`${API_URL}/pets`);
  // pets.value = await respostaPets.json();

  const respostaTutores = await fetch(`${API_URL}/tutores`);
  tutores.value = await respostaTutores.json();
}

function nomeDoTutor(tutorId) {
  for (const tutor of tutores.value) {
    if (tutor.id === tutorId) {
      return tutor.nome;
    }
  }
  return 'Tutor não encontrado';
}

async function excluirTutor(id) {
  const confirmarExclusao = window.confirm('Tem certesa que deseja excluir esse pet?');
  if (confirmarExclusao) {
    await fetch(`${API_URL}/tutores/${id}`,{
      method: 'DELETE',
    });
    await carregarDados();
  }
}
onMounted(carregarDados);
</script>

<template>
  <div>
    <header class="mb-4">
      <h1 class="text-2xl font-bold">Listagem de Tutores</h1>
      <p class="text-body-secondary mb-0">
        Listagem dos Tutores cadastrados no sistema.
      </p>
    </header>
  </div>

  <table class="table table-striped table-hover">
    <thead>
      <tr>
        <th>ID</th>
        <th>Nome</th>
        <th>Telefone</th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="tutor in tutores"
        :key="tutor.id"
      >
        <td>{{ tutor.id }}</td>
        <td>{{ tutor.nome }}</td>
        <td>{{ tutor.telefone }}</td>
        <td>
          <RouterLink
              :to="{ name: 'detalhes-tutor', params: { id: tutor.id } }"> EDITAR </RouterLink>

              <button
                class="btn btn-danger"
                @click="excluirTutor(tutor.id)"> EXCLUIR
              </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>
