<template>
  <div class="mx-auto flex flex-col gap-y-5">
    <div class="flex justify-between">
      <span class="font-bold text-3xl">Work Order Master</span>

      <div class="flex gap-2">
        <input placeholder="Cari Nama" class="p-2 rounded-md debug" />
        <button
          class="bg-gray-800 rounded-md p-2 text-white cursor-pointer hover:bg-gray-700"
        >
          Add
        </button>
      </div>
    </div>

    <div class="flex flex-col gap-4">
      <span class="text-xl font-semibold">General</span>
      <div class="flex flex-col">
        <div
          v-for="data in dataJSON"
          :key="data.id"
          class="flex justify-between items-center border border-gray-300 p-2"
        >
          <div class="flex flex-col">
            <span class="text-blue-500 text-sm font-semibold">{{
              data.type
            }}</span>
            <span class="font-semibold">{{ data.title }}</span>
            <span class="text-gray-400">{{ data.code }}</span>
          </div>
          <div>
            <div>Edit</div>
          </div>
        </div>
      </div>
      <span class="text-xl font-semibold">Equipment for Crew </span>
      <span class="text-xl font-semibold">Hull</span>
      <span class="text-xl font-semibold">Machiney Main Components </span>
      <span class="text-xl font-semibold">Ship Common Systems </span>
    </div>
  </div>
</template>

<script setup>
const dataJSON = ref([]);
const { data, error, pending } = await useFetch(
  "http://localhost:3000/data/work-order.json"
);

dataJSON.value = data.value["work-order"];

console.log(data.value["work-order"]);
</script>
