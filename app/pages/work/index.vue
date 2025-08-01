<template>
  <div class="mx-auto flex flex-col gap-y-5">
    <div class="flex justify-between">
      <span class="font-bold text-3xl">Work Order Master</span>

      <div class="flex gap-2">
        <input
          v-model="search"
          placeholder="Cari Code"
          class="p-2 rounded-md debug"
        />
        <button
          class="bg-gray-800 rounded-md p-2 text-white cursor-pointer hover:bg-gray-700"
        >
          Add
        </button>
      </div>
    </div>

    <div
      v-for="(data, key) in filterItems"
      :key="data.id"
      class="flex flex-col gap-4"
    >
      <span class="text-xl font-semibold">{{ handleTitle(key) }}</span>
      <div v-for="item in data" class="flex flex-col gap-4">
        <div
          @click="$router.push(`/work/${key}/${item.id}`)"
          class="flex flex-col"
        >
          <div
            class="flex justify-between items-center border border-gray-300 p-2"
          >
            <div class="flex flex-col">
              <span class="text-blue-500 text-sm font-semibold">{{
                item.type
              }}</span>
              <span class="font-semibold">{{ item.title }}</span>
              <span class="text-gray-400">{{ item.code }}</span>
            </div>
            <div>
              <div>Edit</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const jsonData = ref([]);
const { data, error, pending } = await useFetch(
  "http://localhost:3000/data/work-order.json"
);
onMounted(() => {
  jsonData.value = data.value;
});

const handleTitle = (title) => {
  switch (title) {
    case "general":
      return "General";
    case "equipment":
      return "Equipment for Crew";
    case "hull":
      return "Hull";
    case "machiney":
      return "Machiney Main Components";
    case "ship":
      return "Ship Common Systems";
    default:
      break;
  }
};

const search = ref("");
const filterItems = computed(() => {
  if (!search.value) {
    return jsonData.value;
  }

  return jsonData.value.filter((data) =>
    data.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>
