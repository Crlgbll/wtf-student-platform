<template>
  <div class="bg-black h-screen w-full relative">
    <Sidebar v-if="isSidebarVisible" />

    <div
      class="font-bold text-2xl h-16 w-full bg-gradient-to-t from-gray-800 via-black to-[#3ED598] p-5"
    >
      <h1>Notifications</h1>
    </div>

    <TabBarMenu @show-sidebar="toggleSidebar" />
  </div>
  z
</template>

<script setup lang="ts">
const isSidebarVisible = ref(false);

const toggleSidebar = () => {
  isSidebarVisible.value = !isSidebarVisible.value;
};
</script>

<style scoped></style>
