<script setup></script>
<template>
  <h1>detalhes de tutor</h1>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { RouterLink, useRoute } from 'vue-router';

// chamando minha UseRouter

const route = useRoute();

// chamando nossa api
const API_URL = 'http://localhost:3000';
// criando variáveis reativas para armazenar os dados do pet e do tutor
//const pet = ref({});
const tutor = ref({});

// função para carregar os dados do pet e do tutor
async function carregarTutor() {
  try {
    const respostaTutor = await fetch(`${API_URL}/tutores/${route.params.id}`);
    if (!respostaTutor.ok) {
      console.log('Yep, Tutor não encontrado!');
    }

    tutor.value = await respostaTutor.json();
    console.log(tutor.value);

    const respostaTutor = await fetch(
      `${API_URL}/tutores/${tutor.value.tutorId}`,
    );
    tutor.value = respostaTutor.ok
      ? await respostaTutor.json()
      : { nome: 'Tutor não encontrado' };
  } catch (erro) {
    console.error('Erro ao carregar os dados do pet e do tutor:', erro);
  }
}

onMounted(carregarTutor);
</script>

<template>
  <p>Tutor: {{ nomeDoTutor(pet.tutorId) }}</p>
</template>
