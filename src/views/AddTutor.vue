Endpoint: Cadastrar tutor Método: POST Ação: /tutores
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

// chamando a minha API para salvar os dados de Tutor
const novoTutor = ref({
  nome: '',
  cpfCnpj: '',
  telefone: '',
  email: '',
  nasc: '',
});

async function salvarTutor() {
  // fazendo uma requisição para o servidor
  await fetch(`${API_URL}/tutores`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(novoTutor.value),
  });
  router.push('/tutores');
}

onMounted(carregarTutores);
</script>

<template>
  <div>
    <header class="mb-4">
      <h1 class="text-2xl font-bold">Cadastro de Tutor</h1>
      <p class="text-body-secondary mb-0">Cadastro de Tutores no sistema.</p>
    </header>

    <!-- dados do tutor-->

    <h2>Dados do Tutor</h2>

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
      <!-- data de nascimento -->
      <div class="col-md-6">
        <label
          for="nasc"
          class="form-label"
          >Data de Nascimento</label
        >
        <input
          type="date"
          id="nasc"
          v-model="novoTutor.nasc"
          class="form-control"
          required
        />
      </div>

      <!-- endereco -->

      <h2>Endereço</h2>

      <!-- cep -->

      <div class="col-md-6">
        <label
          for="cep"
          class="form-label"
          >CEP</label
        >
        <input
          type="number"
          id="cep"
          v-model="novoTutor.cep"
          class="form-control"
          required
        />
      </div>

      <!-- rua -->
      <div class="col-md-6">
        <label
          for="rua"
          class="form-label"
          >Rua</label
        >
        <input
          type="text"
          id="rua"
          v-model="novoTutor.rua"
          class="form-control"
          required
        />
      </div>

      <!-- bairro -->
      <div class="col-md-6">
        <label
          for="bairro"
          class="form-label"
          >Bairro</label
        >
        <input
          type="text"
          id="bairro"
          v-model="novoTutor.bairro"
          class="form-control"
          required
        />
      </div>

      <!-- cidade -->
      <div class="col-md-6">
        <label
          for="cidade"
          class="form-label"
          >Cidade</label
        >
        <input
          type="text"
          id="cidade"
          v-model="novoTutor.cidade"
          class="form-control"
          required
        />
      </div>

      <!-- estado -->
      <div class="col-md-6">
        <label for="estado">Estado:</label>
        <select
          id="estado"
          name="estado"
        >
          <option
            value=""
            selected
            disabled
          >
            Selecione um estado
          </option>
          <option value="AC">Acre</option>
          <option value="AL">Alagoas</option>
          <option value="AP">Amapá</option>
          <option value="AM">Amazonas</option>
          <option value="BA">Bahia</option>
          <option value="CE">Ceará</option>
          <option value="DF">Distrito Federal</option>
          <option value="ES">Espírito Santo</option>
          <option value="GO">Goiás</option>
          <option value="MA">Maranhão</option>
          <option value="MT">Mato Grosso</option>
          <option value="MS">Mato Grosso do Sul</option>
          <option value="MG">Minas Gerais</option>
          <option value="PA">Pará</option>
          <option value="PB">Paraíba</option>
          <option value="PR">Paraná</option>
          <option value="PE">Pernambuco</option>
          <option value="PI">Piauí</option>
          <option value="RJ">Rio de Janeiro</option>
          <option value="RN">Rio Grande do Norte</option>
          <option value="RS">Rio Grande do Sul</option>
          <option value="RO">Rondônia</option>
          <option value="RR">Roraima</option>
          <option value="SC">Santa Catarina</option>
          <option value="SP">São Paulo</option>
          <option value="SE">Sergipe</option>
          <option value="TO">Tocantins</option>
        </select>
      </div>

      <RouterLink
        class="btn btn-primary"
        :to="{ name: 'tutores' }"
      >
        Tutores
      </RouterLink>
      --

      <button
        type="submit"
        class="btn btn-success"
      >
        Salvar Tutor
      </button>
    </form>
  </div>
</template>
