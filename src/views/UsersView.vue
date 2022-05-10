<template>
  <div class="users">
    <transition name="fade">
      <h1 v-if="!hideTitle">Listado de usuarios activos</h1>
    </transition>
    <h2 v-if="hideTitle" @click="hideTitle = false">Titulo oculto</h2>
    <h2 v-else>
      Usuarios
      <span @click="hideTitle = true" :class="activeColor">{{
        users.length
      }}</span>
    </h2>

    <button class="my-button" @click="showForm = !showForm">
      Crear usuario
    </button>
    <div v-if="showForm">
      <form @submit.prevent="submit">
        <input v-model="form.name" />
        <button class="my-button" type="submit">Agregar</button>
      </form>
    </div>
    <p>{{ isOdd }}</p>
    <TransitionGroup name="fade">
      <li v-for="user in users" :key="user.id">
        <user :user="user" @remove="remove" />
      </li>
    </TransitionGroup>
  </div>
</template>
<script setup>
import User from "../components/User.vue";
import _ from "lodash";
import { computed, ref, watch } from "vue";
import { random } from "lodash/number";

let showForm = ref(false);
let form = ref({
  name: "",
});
let users = ref([
  {
    id: 1,
    name: "Pedro",
  },
  {
    id: 2,
    name: "Juan",
  },
]);
let hideTitle = ref(false);
let colors = ref(["blue", "red", "green"]);
let activeColor = ref("blue");
// eslint-disable-next-line vue/return-in-computed-property
const isOdd = computed(() => {
  let txt =
    users.value.length === 0 ||
    !!(users.value.length && !(users.value.length % 2))
      ? "par"
      : "impar";
  return "El numero de usuarios es " + txt;
});
/*const plusOne = computed({
    get: () => users.value + 1,
    set: val => {
        users.value = val - 1
    }
});*/
watch(users.value, (val, oldVal) => {
  let index = random(0, val.length);
  console.log(index);
  activeColor.value = colors.value[index];
});

const submit = () => {
  let id = random(1, 25);
  users.value.push({
    id: id,
    name: form.value.name,
  });
  alert(`Se ha creado el usuario ${form.value.name}`);
  form.value.name = "";
};
const remove = (id) => {
  let index = _.findIndex(users.value, function (o) {
    return o.id === id;
  });
  if (index !== -1) {
    users.value.splice(index, 1);
  }
};
</script>
<style>
.users {
  align-items: center;
}
.my-button {
  padding: 5px;
  background-color: dodgerblue;
  color: white;
  border-radius: 4px;
}
form {
  margin-top: 15px;
  margin-bottom: 15px;
}
input {
  margin-right: 5px;
  height: 30px;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.red {
  color: red;
}
.blue {
  color: blue;
}
.green {
  color: green;
}
</style>
