<template>
  <div class="component">
    <label class="field-label">{{ title }}:</label>
    <input class="field-textbox" type="text" v-model="model">
  </div>
</template>

<script setup>

// eslint-disable-next-line
const model = defineModel();

defineProps({
  title: String
})
</script>

<style scoped>
.component {
  display: flex;
  flex-direction: column;
  padding-block: 10px 10px;
}
.field-label {
  font-size: 12px;
  padding-bottom: 5px;
  opacity: 0.5;
}
.field-textbox {
  font-size: 14px;
  color: #696969;
  font-family: Roboto,sans-serif;
  box-sizing: border-box;
  border: 1px solid #D9DBDA;
  border-radius: 4px;
  padding: 10px 18px 10px 18px;
  transition: 0.5s;
  outline: none;
}
.field-textbox:focus {
  border: 1px solid #555;
}
</style>
