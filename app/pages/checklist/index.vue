<template>
  <div class="mx-auto flex flex-col gap-y-5">
    <div class="flex justify-between">
      <span class="font-bold text-3xl">Checklists</span>

      <div class="flex gap-2">
        <input placeholder="Cari Nama" class="p-2 rounded-md debug" />
        <button
          class="bg-gray-800 rounded-md p-2 text-white cursor-pointer hover:bg-gray-700"
        >
          Add
        </button>
      </div>
    </div>

    <table class="border-collapse border border-gray-400 table-auto w-full">
      <thead class="text-left">
        <tr class="rounded-md bg-gray-300 border border-gray-500">
          <th v-for="col in tableHead" class="p-2">{{ col }}</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in jsonData"
          @click="$router.push(`/checklist/${item.id}`)"
        >
          <td class="p-2">{{ item.name }}</td>
          <td class="p-2">{{ item.description }}</td>
          <td class="p-2">{{ item.active }}</td>
          <td class="p-2">Option</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
const tableHead = ref(["CHECKLIST NAME", "Description", "Active", ""]);

const jsonData = ref([]);
const { data, error, pending } = await useFetch(
  "http://localhost:3000/data/checklist.json"
);
onMounted(() => {
  jsonData.value = data.value["checklist"];
});
</script>
