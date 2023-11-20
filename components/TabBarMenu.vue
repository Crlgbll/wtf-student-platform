<template>
  <div
    class="h-16 w-full border-2 border-gray-500 bg-[#202020] rounded-t-3xl fixed bottom-0 z-20 ease-in-out"
  >
    <div
      class="h-full max-w-lg mx-auto relative flex justify-evenly items-center"
    >
      <button
        :class="{
          'h-14 w-14 rounded-full hover:bg-gray-600': true,
          'bg-[#3DD598]': isSidebarActive,
        }"
        @click="emitShowSidebar"
      >
        <icon size="28" name="fa6-solid:user"></icon>
      </button>
      <button
        :class="{
          'h-14 w-14 rounded-full hover:bg-gray-600': true,
          'bg-[#3DD598]': isActive('/dashboard'),
        }"
      >
        <nuxt-link to="/dashboard">
          <icon size="28" name="fa6-solid:house"></icon>
        </nuxt-link>
      </button>
      <button
        :class="{
          'h-14 w-14 rounded-full hover:bg-gray-600': true,
          'bg-[#3DD598]': isActive('/inbox'),
        }"
      >
        <nuxt-link to="/inbox">
          <icon size="28" name="material-symbols-light:notifications"></icon>
        </nuxt-link>
      </button>
    </div>
  </div>
</template>

<script setup>
const route = useRoute();
const isSidebarActive = ref(false);

const emit = defineEmits(["show-sidebar"]);
const emitShowSidebar = () => {
  isSidebarActive.value = !isSidebarActive.value;
  emit("show-sidebar");
};
const isActive = (path) => route.path === path;
</script>

<style lang="scss" scoped></style>
