<template>
  <div class="mx-auto flex flex-col gap-y-5"></div>
</template>

<script setup>
const route = useRoute();
const key = route.params.key;
const id = route.params.id;

const jsonData = ref([]);
const profile = ref();

const { data, error, pending } = await useFetch("/data/work-order.json");
</script>
