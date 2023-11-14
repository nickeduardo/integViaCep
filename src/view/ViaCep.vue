
<template>
    <div>
        <h1>Consultar CEP</h1>
        <hr>
        <form action="#" onsubmit="event.preventDefault()">
            <label for="cep">Digite o CEP: </label>
            <input type="text" id="cep" v-model="cep">
            <input type="submit" value="Consultar" @click="getCep">
        </form>
        <div>
            <p>Rua: {{ place.street }} </p>
            <p>Bairro: {{ place.neighborhood }} </p>
            <p>Cidade: {{ place.city }}-{{ place.state }} </p>
        </div>


    </div>
</template>

<script setup>
import axios from 'axios'
import { reactive, ref } from 'vue';

const baseUrl = 'https://viacep.com.br/ws/'
const format = '/json'

const cep = ref()

const place = reactive({
    street : '',
    neighborhood : '',
    city : '',
    state : ''
})

const getCep = () => {
    axios.get(baseUrl + cep.value + format)
    .then( (response) => {
        console.log(response)
        /* como saber os nomes dos atributos? olhando a documentação da API (...) -> https://viacep.com.br/ */
        place.street = response.data.logradouro, 
        place.neighborhood = response.data.bairro,
        place.city = response.data.localidade,
        place.state = response.data.uf
    })
    .catch ( (error) => {
        console.error('Ocorreu um erro: ', error)
    })
}

</script>

<style scoped>

</style>
