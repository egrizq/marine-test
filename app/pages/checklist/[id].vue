<template>
  <div class="mx-auto flex flex-col gap-y-5">
    <div class="flex justify-between">
      <div class="flex flex-col">
        <span class="font-bold text-3xl">{{ nameModel }}</span>
        <span class="text-gray-500">{{ descModel }}</span>
      </div>
    </div>

    <div class="flex gap-4">
      <div class="flex flex-col gap-2 w-full">
        <label>Checklist Name</label>
        <input
          v-model="nameModel"
          class="debug rounded-md border-white bg-white text-black"
        />
      </div>
      <div class="flex flex-col gap-2 w-full">
        <label>Description</label>
        <input
          v-model="descModel"
          class="debug rounded-md border-white bg-white text-black"
        />
      </div>
      <div class="flex flex-col gap-2 w-full">
        <label>ACTIVE </label>
        <div class="flex gap-2">
          <span class="w-64"
            >Only Active Checklists will be available in work orders</span
          >
          <input
            v-model="activeModel"
            type="checkbox"
            class="debug rounded-md border-white bg-white text-black"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const route = useRoute();
const id = route.params.id;

const jsonData = ref();
const { data, error, pending } = await useFetch(
  "http://localhost:3000/data/checklist.json"
);
jsonData.value = data.value["checklist"][id - 1];

const nameModel = ref(jsonData.value.name);
const descModel = ref(jsonData.value.description);
const activeModel = ref(jsonData.value.active);
</script>
