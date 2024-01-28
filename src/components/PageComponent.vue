<template>
  <HeaderComponent class="header" title="USERS"/>
  <hr class="separator"/>
  <AccordionContainer class="accordion-font" v-if="users" :arr="users"/>
</template>

<script setup>
import AccordionContainer from "./Accordion/AccordionContainer";
import {ref, watchEffect} from "vue";
import HeaderComponent from "./HeaderComponent";

const users = ref(null);

watchEffect(async () => {
  const url = 'https://jsonplaceholder.typicode.com/users'
  users.value = await (await fetch(url)).json()
})
</script>

<style scoped>
.accordion-font {
  font-size: 14px;
  font-family: Roboto, sans-serif;
  color: #696969;
}
.header {
  font-size: 20px;
  font-family: Roboto, sans-serif;
  color: #696969;
  font-weight: 500;
  display: flex;
  padding: 0 0 20px 50px;
}
.separator {
  border-top: 1px solid #727270;
  opacity: 0.2;
}
</style>
