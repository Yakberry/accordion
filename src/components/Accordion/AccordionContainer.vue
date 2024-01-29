<template>
  <div class="accordion">
    <div class="head">
      <span>Name</span>
      <span>Email</span>
      <span>Phone</span>
      <span>Website</span>
    </div>
    <div v-for="(item, index) in arr" :key="item" class="box" >
      <AccordionItem :item="item" :show-form="showIndex === index" :expand="onExpand(index)"/>
    </div>
  </div>
</template>

<script setup>
import AccordionItem from "./AccordionItem";
import {ref} from "vue";

defineProps({
  arr: Array
})

const showIndex = ref(null);

const onExpand = (index) => {
  return () => {
    if (showIndex.value === index) {
      showIndex.value = null
      return
    }
    showIndex.value = index;
  }
}
</script>

<style scoped>
.accordion {
  padding-inline: 40px 40px;
}
.accordion .box {
  position: relative;
  margin: 10px 20px;
}
.head {
  position: relative;
  padding: 10px 12px 0 62px;
  margin-inline: 20px 20px;
  display: flex;
  font-size: 12px;
  opacity: 0.5;
}
.head > span {
  flex: 1;
  text-align: left;
}
</style>
