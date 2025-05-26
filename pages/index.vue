<template>
    <div>
        <h1>Buscar Endereço por CEP</h1>

        <!-- v-model faz com que o valor digitado será automaticamente salvo na variável 'cep' -->
        <input v-model="cep" type="number" placeholder="Digite o CEP" />

        <button @click="buscarEndereco">Buscar</button>

        <!-- v-if exibe a div somente se a variável 'endereco' tiver algum valor (não for null ou undefined) -->
        <div v-if="endereco">
            <p>Logradouro: {{ endereco.logradouro }}</p>
            <p>Bairro: {{ endereco.bairro }}</p>
            <p>Cidade: {{ endereco.localidade }}</p>
            <p>Estado {{ endereco.estado }}</p>
        </div>
    </div>
</template>

<script setup>
import { ref } from "vue";

// ref faz um objeto reativo, permitindo que o Vue "observe" esse valor e reaja automaticamente a mudanças
const cep = ref("");
const endereco = ref(null);

async function buscarEndereco() {
    const response = await $fetch(`https://viacep.com.br/ws/${cep.value}/json/`);
    endereco.value = response;
}
</script>
