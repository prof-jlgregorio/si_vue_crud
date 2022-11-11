<template>
    <div>
        <h1>Cadastrar Nova Profissão</h1>
        <input type="text" name="name" id="name" v-model="profession.name">
        <button @click="save()">Salvar</button>
    </div>
</template>

<script setup>
import { reactive } from "@vue/reactivity";
import axios from "axios";
import env from "/env.json"


    const apiURL = env.apiURL

    const profession = reactive({
        name: ""
    })

    const save = () => {
        axios.post(apiURL + "/profession", profession)
        .then((response) => {
            if(response.status === 200){
                profession.name = ""
                alert("Dados Cadastrados com sucesso!")                
            }
        }).catch( (error) => {
            alert("Erro: " + error.response.status)
        } )
    }

</script>

<style lang="scss" scoped>

</style>