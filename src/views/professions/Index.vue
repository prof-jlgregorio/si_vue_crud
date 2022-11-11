<template>
  <div>
    <h1>Profissões Cadastradas</h1>
    <hr />
    <table border="1">
      <tr>
        <th>Nome</th>
        <th>Editar</th>
        <th>Excluir?</th>
      </tr>
      <tr v-for="p in professions">
        <td>{{ p.name }}</td>
        <td>
          <router-link :to="{ name: 'pro-edit', params: { id: p.id } }"
            >Editar</router-link
          >
        </td>
        <td><button @click="destroy(p.id)">Excluir</button></td>
      </tr>
    </table>
  </div>
</template>

<script setup>
import env from "/env.json";
import { onMounted, ref } from "@vue/runtime-core";
import axios from "axios";

const apiURL = env.apiURL;

const professions = ref([]);

const findAll = () => {
  axios
    .get(apiURL + "/profession")
    .then((response) => {
      professions.value = response.data;
    })
    .catch((error) => {
      alert("Erro: " + error.response.status);
    });
};

const destroy = (id) => {
  if (confirm("Deseja excluir a profissão selecionada?")) {
    axios
      .delete(apiURL + "/profession/" + id)
      .then((response) => {
        if (response.status === 200 && response.data == "") {
          alert("Dados Excluídos com sucesso!");
          findAll();
        }
      })
      .catch((error) => {
        alert("Erro: " + error.response.status);
      });
  }
};

onMounted(() => {
  //console.log("URL: " + url)
  findAll();
  console.log("data: " + professions.value);
});
</script>

<style lang="scss" scoped></style>
