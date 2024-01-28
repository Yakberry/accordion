<template>
  <div class="head" @click="expand">
    <span>{{ item.name }}</span>
    <span>{{ item.email }}</span>
    <span>{{ item.phone }}</span>
    <span>{{ item.website }}</span>
  </div>
  <div class="form-container">
    <UserForm :item="item" v-if="showForm"/>
  </div>
</template>

<script setup>
import UserForm from "../UserForm/UserForm";
defineProps({
  item: Object,
  showForm: Boolean,
  expand: Function
})
</script>

<style scoped>
.head {
  position: relative;
  padding: 10px 10px 10px 60px;
  cursor: pointer;
  border: solid 2px #FFD200;
  display: flex;
  flex-direction: row;
}

.head > span {
  flex: 1;
  text-align: left;
}

.head::before {
  content: url("../../assets/shevron.svg");
  position: absolute;
  top: 50%;
  left: 20px;
  transform: translateY(-50%);
  font-size: 1.5em;
}

.form-container {
  transition: height .5s;
  height: 500px;
  overflow: hidden;
}

.form-container:empty {
  height: 0;
}

</style>
