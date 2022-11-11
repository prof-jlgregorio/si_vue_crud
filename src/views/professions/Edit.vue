<template>
    <div>
        <h1>Editar Profissão</h1>
        <input type="text" name="name" id="name" v-model="profession.name">
        <button @click="update">Salvar</button>
    </div>
</template>

<script setup>
import { onMounted, ref } from "vue"
import env from "/env.json"
import { useRoute } from "vue-router";
import axios from "axios";

const apiURL = env.apiURL

const route = useRoute()

const profession = ref({ id: null, name : "" })

const load = () => {
    let id = route.params.id
    axios.get(apiURL + "/profession/" + id)
    .then((response) => {
        profession.value.id = response.data.id;
        profession.value.name = response.data.name;
    }).catch((error) => {
        alert("Erro: " + error.response.status)
    })
}

const update = () => {
    axios.put(apiURL + "/profession", profession.value)
    .then((response) => {
        if(response.data != ""){
            alert("Dados atualizados com sucesso!")
            load()
        }
    }).catch((error) => {
        alert("Erro: " + error.response.status)
    })
}

onMounted(() => {
    load();
})

</script>

<style lang="scss" scoped>

</style>