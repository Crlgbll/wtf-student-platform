<template>
  <div v-if="pending">
    <Skeleton_Sidebar />
  </div>
  <div class="h-full w-52 bg-[#1A1919] absolute top-0 left-0 z-10">
    <div class="flex h-1/3 w-full mt-6 px-3 items-start justify-between">
      <button
        class="h-12 w-12 rounded-full bg-[#3ED598] hover:scale-105 ease-in-out top-0"
      >
        <icon name="fluent-emoji-flat:boy-light" />
      </button>
      <div class="flex flex-col justify-center">
        <h1 class="font-bold w-32">
          {{ student?.student?.first_name + " " + student?.student?.last_name }}
        </h1>
        <p class="text-xs">{{ student?.student?.program?.program_name }}</p>
      </div>
    </div>
    <div class="flex flex-col items-start px-5 gap-3">
      <button class="text-[#96A7AF]">
        <icon name="material-symbols:settings"></icon> Settings
      </button>
      <button
        class="font-bold h-10 w-24 bg-[#40DF9F] text-[#006C68] hover:bg-[#006C68] hover:text-[#40DF9F] rounded-xl"
      >
        Logout
      </button>
    </div>
    <div class=""></div>
  </div>
</template>

<script setup>
const isSidebarVisible = ref(false);

const toggleSidebar = () => {
  isSidebarVisible.value = !isSidebarVisible.value;
};

const { data: student, pending } = useFetch(
  "https://wtf-backend-production.up.railway.app/api/student/211-00121"
);
</script>

<style lang="scss" scoped></style>
