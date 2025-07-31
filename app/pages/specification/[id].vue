<template>
  <div class="flex flex-col gap-5 w-full">
    <div>
      <span class="text-2xl font-semibold">{{ profile.name }}</span>
    </div>

    <div class="grid grid-cols-3 gap-4">
      <div class="flex flex-col">
        <span class="text-gray-600 text-xl">Vessel</span>
        <span>{{ profile.vessel }}</span>
      </div>
      <div class="flex flex-col">
        <span class="text-gray-600 text-xl">Group No. </span>
        <span>{{ profile.group }}</span>
      </div>
      <div class="flex flex-col">
        <span class="text-gray-600 text-xl">Name</span>
        <span>{{ profile.name }}</span>
      </div>
      <div class="flex flex-col">
        <span class="text-gray-600 text-xl">Sort Order </span>
        <span>{{ profile.sort }}</span>
      </div>
    </div>

    <NuxtLink
      to="/specification"
      class="debug w-fit p-2 text-white rounded-md bg-gray-800"
      >Back</NuxtLink
    >
  </div>
</template>

<script setup>
const route = useRoute();
const id = route.params.id;

const jsonData = ref([]);
const profile = ref();

const { data, error, pending } = await useFetch("/data/specification.json");
jsonData.value = data.value["specification"];
profile.value = jsonData.value[id - 1];

console.log(profile.value.name);
</script>
