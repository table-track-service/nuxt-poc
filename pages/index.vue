<template>
    <div>
        <h1>Buscar Endereço por CEP</h1>

        <!-- v-model faz com que o valor digitado será automaticamente salvo na variável 'cep' -->
        <input v-model="cep" type="text" placeholder="Digite o CEP" />

        <button @click="buscarEndereco">Buscar</button>

        <div v-if="erro"> {{ erro }}</div>

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
const erro = ref("")

async function buscarEndereco() {
    const cepLimpo = cep.value.replace(/\D/g, "");

    if (cepLimpo.length !== 8) {
        erro.value = "Insira um CEP com 8 digitos"
        endereco.value = ""
        return
    }

    try {
        const response = await $fetch(`https://viacep.com.br/ws/${cepLimpo}/json/`)

        if (response.erro) {
            erro.value = "CEP nao encontrado"
            endereco.value = ""
        } else {
            endereco.value = response;
            erro.value = ""
        }
    } catch (e) {
        erro.value = "Erro ao buscar o endereco"
        endereco.value = ""
    }
}
</script>
