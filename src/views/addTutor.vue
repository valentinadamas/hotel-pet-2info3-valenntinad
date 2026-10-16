 Endpoint: Cadastrar tutor
Método: POST
Ação: /tutores
<script setup>
import { onMounted, ref } from 'vue';
import { RouterLink, useRouter } from 'vue-router';

// chamando a minha API para exibir os dados de Tutor
const API_URL = 'http://localhost:3000';
const router = useRouter();

// exibindo a lista de tutores da aplicação
const tutores = ref([]);

async function carregarTutores() {
  const resposta = await fetch(`${API_URL}/tutores`);
  console.log('tutores', resposta.json);
  // tranformando os valores da minha API para o formato JSON
  tutores.value = await resposta.json();
}

// chamando a minha API para salvar os dados de Pet
const novoPet = ref({
  nome: '',
  especie: '',
  tutorId: '',
});

async function salvarPet() {
  // fazendo uma requisição para o servidor
  await fetch(`${API_URL}/pets`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(novoPet.value),
  });
  router.push('/pets');
}

onMounted(carregarTutores);
</script>

<template>
  <div>
    <header class="mb-4">
      <h1 class="text-2xl font-bold">Cadastro de Tutor</h1>
      <p class="text-body-secondary mb-0">Cadastro de Tutores no sistema.</p>
    </header>
    <!--
    <RouterLink
      class="btn btn-primary"
      :to="{ name: 'addPet' }"
    >
      Adicionar Pet
    </RouterLink> -->

    <form @submit.prevent="salvarTutor">
      <!-- nome -->
      <div class="col-md-6">
        <label
          for="nome"
          class="form-label"
          >Nome do Tutor:</label
        >
        <input
          type="text"
          id="nome"
          v-model="novoTutor.nome"
          class="form-control"
          required
        />
      </div>
      <!-- cpf ou cnpj -->
        <div class="col-md-6">
        <label
          for="cpfCnpj"
          class="form-label"
          >CPF/CNPJ</label
        >
        <input
          type="number"
          id="cpfCnpj"
          v-model="novoTutor.cpfCnpj"
          class="form-control"
          required
        />
      </div>
      <!-- telefone -->
        <div class="col-md-6">
        <label
          for="telefone"
          class="form-label"
          >Telefone</label
        >
        <input
          type="number"
          id="telefone"
          v-model="novoTutor.telefone"
          class="form-control"
          required
        />
      </div>
      <!-- email -->
        <div class="col-md-6">
        <label
          for="email"
          class="form-label"
          >Email</label
        >
        <input
          type="email"
          id="email"
          v-model="novoTutor.email"
          class="form-control"
          required
        />
      </div>

      <button
        type="submit"
        class="btn btn-success"
      >
        Salvar Pet
      </button>
    </form>
  </div>
</template>
