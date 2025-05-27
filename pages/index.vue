<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center p-4">
    <div class="bg-white shadow-md rounded-2xl p-8 w-full max-w-md space-y-6">
      <h1 class="text-2xl font-bold text-center">
        Buscar Endereço por CEP
      </h1>

      <input
        v-model="cep"
        type="text"
        placeholder="Digite o CEP"
        class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
      />

      <button
        @click="buscarEndereco"
        class="w-full bg-blue-600 text-white p-3 rounded-lg hover:bg-blue-700"
      >
        Buscar
      </button>

      <div v-if="erro" class="text-red-600 text-center">
        {{ erro }}
      </div>

      <div v-if="endereco" class="text-gray-700 space-y-2">
        <p><strong>Logradouro:</strong> {{ endereco.logradouro }}</p>
        <p><strong>Bairro:</strong> {{ endereco.bairro }}</p>
        <p><strong>Cidade:</strong> {{ endereco.localidade }}</p>
        <p><strong>Estado:</strong> {{ endereco.uf }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const cep = ref("");
const endereco = ref(null);
const erro = ref("");

async function buscarEndereco() {
  const cepLimpo = cep.value.replace(/\D/g, "");

  if (cepLimpo.length !== 8) {
    erro.value = "Insira um CEP com 8 dígitos";
    endereco.value = "";
    return;
  }

  try {
    const response = await $fetch(`https://viacep.com.br/ws/${cepLimpo}/json/`);

    if (response.erro) {
      erro.value = "CEP não encontrado";
      endereco.value = "";
    } else {
      endereco.value = response;
      erro.value = "";
    }
  } catch (e) {
    erro.value = "Erro ao buscar o endereço";
    endereco.value = "";
  }
}
</script>