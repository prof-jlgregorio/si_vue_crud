<script setup>
import Home from '@/views/Home.vue';
</script>

<template>
  <div>
    <h1>Front-End App</h1>
    <ul>
      <li> <router-link to="/">Início</router-link> </li>
      <li> Profissões
        <ul>
          <li> <router-link to="/professions">Listar Profissões</router-link> </li>
          <li> <router-link to="/professions/create">Cadastrar</router-link> </li>
        </ul>
      </li>
    </ul>
    <router-view />
  </div>
</template>

<style scoped>

</style>
