<template>
  <div class="about">
    <h2 class="">Contador {{ counter }}</h2>
    <div>
      <button
        class="my-button"
        style="margin-left: 35px"
        type="button"
        @click="increment"
      >
        Incrementar
      </button>
    </div>
  </div>
</template>
<script setup>
import { useCounterStore } from "../stores/counter";
import { storeToRefs } from "pinia/dist/pinia";
const { counter } = storeToRefs(useCounterStore());
const { increment } = useCounterStore();
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
