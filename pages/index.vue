<template>
    <div>
        <h1>Buscar Endereço por CEP</h1>

        <!-- v-model faz com que o valor digitado será automaticamente salvo na variável 'cep' -->
        <input v-model="cep" type="number" placeholder="Digite o CEP" />

        <button @click="">Buscar</button>

        <!-- v-if exibe a div somente se a variável 'endereco' tiver algum valor (não for null ou undefined) -->
        <div v-if="endereco">
            <p>Logradouro: {{}}</p>
            <p>Bairro: {{}}</p>
            <p>Cidade: {{}}</p>
            <p>Estado: {{}}</p>
        </div>
    </div>
</template>

<script setup></script>
