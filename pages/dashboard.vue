<template>
  <div v-if="pending">
    <Skeleton_Dashboard />
  </div>
  <div class="h-full w-full bg-black">
    <Sidebar v-if="isSidebarVisible" />
    <img
      class="h-1/3 w-full absolute"
      src="~/assets/images/dashboard-bg.png"
      alt=""
    />
    <div class="h-1/6 w-full relative flex flex-col">
      <div
        class="flex h-1/3 w-full px-4 mt-5 items-center justify-between gap-2"
      >
        <button
          class="h-12 w-12 rounded-full bg-[#3ED598] hover:scale-105 ease-in-out"
        >
          <icon name="fluent-emoji-flat:boy-light" />
        </button>
        <div class="flex flex-col justify-center">
          <h1 class="font-bold w-32">
            {{
              student?.student?.first_name + " " + student?.student?.last_name
            }}
          </h1>
          <p class="text-xs">{{ student?.student?.program?.program_name }}</p>
        </div>
        <div class="h-12 w-1/2 flex justify-end items-center">
          <h1
            class="h-8 w-24 text-sm rounded-full bg-[#252525] hover:bg-[#5CE199] text-[#5CE199] hover:text-[#252525] border-2 border-[#404040] flex justify-center items-center font-bold"
          >
            {{ student?.student?.student_id }}
          </h1>
        </div>
      </div>
      <div class="w-full h-1/2 p-4">
        <h1 class="text-md lg:text-3xl font-bold">
          Check your current balance and updates
        </h1>
      </div>
    </div>
    <div class="flex flex-col lg:flex-row h-[300px] w-full">
      <div class="flex flex-col h-44 xs:w-1/3 items-center relative">
        <CardsCurrentBal />
      </div>
      <div class="h-28 w-full flex justify-center items-center gap-4">
        <CardsLSGTotal />
        <CardsTotalPaid />
      </div>
    </div>
    <Transactions />

    <TabBarMenu @show-sidebar="toggleSidebar" />
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

<style scoped></style>
