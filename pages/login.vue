<template>
  <div
    class="h-screen w-full bg-black font-Poppins text-white flex flex-col items-center justify-center relative"
  >
    <img
      class="h-screen w-full bg-fixed absolute"
      src="~/assets/images/login-bg.png"
      alt=""
    />
    <div
      class="xxxxs:w-full xxxs:w-full xxs:w-full xs:w-4/5 md:w-4/6 lg:w-2/5 xl:w-2/4 mt-6 p-10 bg-black/70 rounded-xl relative border-2 border-gray-700"
    >
      <div class="flex justify-around items-center h-24 w-full">
        <img
          class="h-8 w-48"
          src="~/assets/images/wtf-logo-gray.png"
          alt="WTF Logo"
        />
        <Icon name="ph:x-bold"></Icon>
        <img class="h-20 w-20" src="~/assets/images/ccis-logo.png" alt="" />
      </div>
      <h1 class="text-4xl font-bold my-10 text-center">Login</h1>
      <form class="flex flex-col gap-4">
        <div class="flex flex-col sm:flex-row gap-5">
          <input
            v-for="field in nameFields"
            :key="field.key"
            type="text"
            :id="field.id"
            :placeholder="field.placeholder"
            class="w-full sm:w-1/2 bg-white/0 border-2 border-gray-400 text-sm rounded-lg p-2.5"
            v-model="formData[field.key]"
          />
        </div>

        <input
          v-for="field in inputFields"
          :key="field.key"
          type="text"
          :id="field.id"
          :placeholder="field.placeholder"
          class="w-full bg-white/0 border-2 border-gray-400 text-sm rounded-lg p-2.5"
          v-model="formData[field.key]"
        />

        <div
          class="flex flex-col-reverse h-16 w-full justify-around items-center"
        >
          <NuxtLink to="/register"> Don't have an account? </NuxtLink>
          <button
            class="h-12 w-72 bg-green-500 rounded-xl self-center text-xl"
            @click="submitForm"
            type="submit"
          >
            Login
          </button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      formData: {
        studentId: "",
        password: "",
      },

      inputFields: [
        { id: "student_id", placeholder: "Student ID", key: "studentId" },
        { id: "password", placeholder: "Password", key: "password" },
      ],
    };
  },
};
</script>

<style scoped>
/* You can add custom styles for responsiveness here if needed */
</style>
