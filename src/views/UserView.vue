<template>
  <div class="about">
    <h1>Pagina del usuario {{ $route.params.id }}</h1>
  </div>
</template>
<script setup>
import { onMounted } from "vue";

onMounted(() => {
  console.log("mounted!");
});
</script>
<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
