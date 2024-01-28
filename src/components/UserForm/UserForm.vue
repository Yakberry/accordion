<template>
  <div class="body">
    <div class="bodybox">
      <div class="grid">
        <div class="grid-adress-head grid-element">
          <label> ADDRESS </label>
        </div>
        <div class="grid-company-head grid-element">
          <label> COMPANY </label>
        </div>
        <div class="grid-basic-head grid-element">
          <label> BASIC INFO </label>
        </div>
        <div class="grid-adress-body grid-element">
          <FieldComponent :title="fieldLabels.street" v-model="formData.address.street"/>
          <FieldComponent :title="fieldLabels.suite" v-model="formData.address.suite"/>
          <FieldComponent :title="fieldLabels.city" v-model="formData.address.city"/>
          <FieldComponent :title="fieldLabels.zipcode" v-model="formData.address.zipcode"/>
        </div>
        <div class="grid-company-body grid-element">
          <FieldComponent :title="fieldLabels.name" v-model="formData.company.name"/>
          <FieldComponent :title="fieldLabels.catchphrase" v-model="formData.company.catchPhrase"/>
          <FieldComponent :title="fieldLabels.bs" v-model="formData.company.bs"/>
        </div>
        <div class="grid-basic-body grid-element">
          <FieldComponent :title="fieldLabels.name" v-model="formData.name"/>
          <FieldComponent :title="fieldLabels.username" v-model="formData.username"/>
          <FieldComponent :title="fieldLabels.email" v-model="formData.email"/>
          <FieldComponent :title="fieldLabels.phone" v-model="formData.phone"/>
          <FieldComponent :title="fieldLabels.website" v-model="formData.website"/>
        </div>
      </div>
    </div>
    <img class="tick-button" @click="submit" alt="tick" src="../../assets/tick.svg">
  </div>
</template>

<script setup>
import {ref} from "vue";
import FieldComponent from "@/components/UserForm/FieldComponent";

const props = defineProps({
  item: Object
})

const formData = ref({
  name: props.item.name || "",
  username: props.item.username || "",
  company: { ...props.item.company || {} },
  address: { ...props.item.address || {} },
  email: props.item.email || "",
  phone: props.item.phone || "",
  website: props.item.website || ""
});

const fieldLabels = {
  name: "Name",
  username: "Username",
  company: "Company",
  address: "Address",
  email: "Email",
  phone: "Phone",
  website: "Website",
  street: "Street",
  suite: "Suite",
  city: "City",
  zipcode: "Zipcode",
  catchphrase: "CatchPhrase",
  bs: "Bs"
}

function submit() {
  const changedObjects = [];

  Object.keys(formData.value).forEach((key) => {
    if (
        typeof props.item[key] === "object" &&
        Object.keys(props.item[key]).some((childKey) => props.item[key][childKey] !== formData.value[key][childKey])
    ) {
      changedObjects.push(key);
      return;
    }

    if (typeof props.item[key] === "string" && formData.value[key] !== props.item[key]) {
      changedObjects.push(key);
    }
  });

  if (changedObjects.length === 0) {
    alert("No fields were changed");
    return;
  }

  alert(`${changedObjects.map((key) => {
    const oldValue = props.item[key];
    const newValue = formData.value[key];
    const label = fieldLabels[key];

    if (typeof props.item[key] === "object") {
      const changedChildren = Object.keys(oldValue).filter(
          (childKey) => oldValue[childKey] !== newValue[childKey]
      );
      return `${label}: ${changedChildren.map((childKey) => oldValue[childKey]).join(", ")} -> ${changedChildren.map((childKey) => newValue[childKey]).join(", ")}`;
    }

    return `${label}: ${oldValue} -> ${newValue}`;
  }).join('\n')}`)
}
</script>

<style scoped>
.body {
  position: relative;
  display: flex;
  overflow: hidden;
  padding: 10px;
  overflow-y: auto;
  justify-content: center;
}
.tick-button {
  height: 20px;
  width: 20px;
  padding: 10px;
  margin: 10px 20px 0 30px;
  background: #FFD300;
  border-radius: 4px;
}
.bodybox {
  display: flex;
  flex-direction: column;
  width: 90%;
  padding: 10px;
}
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(1, 1fr);
  grid-column-gap: 0;
  grid-row-gap: 0;
  gap: 1px;
  background: #D9DBDA;
  border: 1px solid #D9DBDA;
}

.grid .grid-element {
  background: white;
  display: flex;
  flex-direction: column;
  text-align: left;
  padding: 10px 30px 10px 30px;
}

.grid-adress-head { grid-area: 1 / 1 / 2 / 2; }
.grid-company-head { grid-area: 1 / 2 / 2 / 3; }
.grid-basic-head { grid-area: 1 / 3 / 2 / 4; }
.grid-adress-body { grid-area: 2 / 1 / 9 / 2; }
.grid-company-body { grid-area: 2 / 2 / 9 / 3; }
.grid-basic-body { grid-area: 2 / 3 / 9 / 4; }
</style>
