<template>
  <div v-if="isOpen" class="w-64 bg-gray-800 text-white p-4">
    <div class="flex justify-between">
      <h2 class="text-xl font-bold mb-4">Dry Dock</h2>

      <button @click="toggleSideBar" class="cursor-pointer">Hide</button>
    </div>
    <ul class="space-y-2">
      <li v-for="r in listRoute">
        <NuxtLink
          :to="`${r.link}`"
          class="hover:underline"
          exact-active-class="text-blue-400 font-semibold pl-2"
          >{{ r.name }}</NuxtLink
        >
      </li>
    </ul>
  </div>

  <div v-else class="w-16 bg-gray-800 text-white p-4">
    <button @click="toggleSideBar" class="cursor-pointer">Hide</button>
  </div>
</template>

<script setup>
const isOpen = ref(true);
const toggleSideBar = () => (isOpen.value = !isOpen.value);

const route = useRoute();

const listRoute = ref([
  {
    link: "/",
    name: "Dashboard",
  },
  {
    link: "/specification",
    name: "Specification",
  },
  {
    link: "/work",
    name: "Work Order Master",
  },
  {
    link: "/checklist",
    name: "Checklist",
  },
  {
    link: "/dry",
    name: "Dry Docks",
  },
]);
</script>
