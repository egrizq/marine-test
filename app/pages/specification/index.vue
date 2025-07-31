<template>
  <div class="mx-auto flex flex-col gap-y-5">
    <div class="flex justify-between">
      <span class="font-bold text-3xl">Specification Groups </span>

      <div class="flex gap-2">
        <input
          v-model="search"
          placeholder="Cari Nama"
          class="p-2 rounded-md debug"
        />
        <button
          @click="togglePane"
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
          v-for="data in filterItems"
          :key="data.id"
          class="cursor-pointer hover:bg-gray-100 hover:bg-gray-200"
          @click="$router.push(`/specification/${data.id}`)"
        >
          <td class="p-2">{{ data.name }}</td>
          <td class="p-2">{{ data.vessel }}</td>
          <td class="p-2">{{ data.group }} dd</td>
          <td class="p-2 cursor-pointer">
            <img src="/images/theedot.png" width="40" height="15" />
          </td>
        </tr>
      </tbody>
    </table>

    <div class="text-center w-full text-3xl">
      <span v-if="filterItems.length === 0">No Data found!</span>
      <span v-else-if="pending">Loading...</span>
      <span v-else-if="error">Error retrieving data</span>
    </div>

    <div
      v-if="isOpen"
      class="w-64 bg-gray-800 text-white p-4 absolute right-0 top-0 h-full"
    >
      <div class="flex justify-between items-center">
        <h2 class="text-xl font-bold">Add Item</h2>
        <button @click="togglePane" class="cursor-pointer">X</button>
      </div>

      <div class="flex flex-col gap-2 pt-5">
        <div class="flex flex-col gap-2">
          <label class="text-white">Vessel</label>
          <select
            v-model="vesselModel"
            class="border rounded-md border-white bg-white text-black"
          >
            <option disabled value="">Please select one</option>
            <option>MV Glory</option>
            <option>MV Ocean</option>
            <option>MV Ocean, MV Glory</option>
          </select>
        </div>
        <div class="flex flex-col gap-2">
          <label class="text-white">Group No.</label>
          <input
            v-model="groupModel"
            type="text"
            class="border rounded-md border-white bg-white text-black"
          />
        </div>
        <div class="flex flex-col gap-2">
          <label class="text-white">Name</label>
          <input
            v-model="nameModel"
            type="text"
            class="border rounded-md border-white bg-white text-black"
          />
        </div>
        <div class="flex flex-col gap-2">
          <label class="text-white">Sort Order</label>
          <input
            v-model="sortModel"
            type="number"
            class="border rounded-md border-white bg-white text-black"
          />
        </div>

        <div class="flex gap-4">
          <button
            @click="submitData"
            class="bg-green-600 rounded-md p-2 text-white cursor-pointer hover:bg-green-700"
          >
            Send
          </button>
          <button @click="togglePane" class="cursor-pointer">Batal</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const tableHead = ref(["Name", "Vessel", "Group No", ""]);

const jsonData = ref([]);
const { data, error, pending } = await useFetch(
  "http://localhost:3000/data/specification.json"
);
jsonData.value = data.value["specification"];

const search = ref("");
const filterItems = computed(() => {
  if (!search.value) {
    return (jsonData.value = data.value["specification"]);
  } else {
    return jsonData.value.filter((data) =>
      data.name.toLowerCase().includes(search.value.toLowerCase())
    );
  }
});

const isOpen = ref(false);
const togglePane = () => (isOpen.value = !isOpen.value);

const vesselModel = ref("");
const groupModel = ref("");
const nameModel = ref("");
const sortModel = ref("");

const submitData = () => {
  jsonData.value.push({
    id: jsonData.value.length + 1,
    vessel: vesselModel.value,
    group: groupModel.value,
    name: nameModel.value,
    sort: sortModel.value,
  });

  vesselModel.value = "";
  groupModel.value = "";
  nameModel.value = "";
  sortModel.value = "";

  isOpen.value = false;
};
</script>
