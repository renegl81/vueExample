<template>
    <h3><router-link :to="{name:'user', params:{id:user.id}}">{{ props.user.name }}</router-link></h3>
  <button @click="remove(props.user.id)">Remove</button>
</template>

<script setup>
const props = defineProps({
  user: Object,
});

const emit = defineEmits(["remove"]);
const remove = (id) => {
  emit("remove", id);
};
</script>

<style scoped>

</style>
