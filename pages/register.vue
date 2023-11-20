<template>
  <div
    class="h-screen w-full bg-black font-Poppins text-white flex justify-center items-center"
  >
    <img
      class="h-screen w-full bg-fixed absolute"
      src="~/assets/images/login-bg.png"
      alt=""
    />
    <div
      class="h-[650px] xs:w-4/5 md:w-4/6 lg:w-2/5 xl:w-2/4 mt-6 p-10 bg-black/70 rounded-xl relative border-2 border-gray-700 max-h-[600px] overflow-y-auto"
      @submit.prevent="submitForm"
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
      <h1 class="text-4xl font-bold my-10 text-center">Register</h1>
      <form class="flex flex-col gap-4 max-h-[600px] overflow-y-auto">
        <input
          required
          v-for="data in student"
          :key="data.key"
          type="text"
          :id="data.id"
          :placeholder="data.placeholder"
          class="w-full bg-white/0 border-2 border-gray-400 text-sm rounded-lg p-2.5"
          v-model="formData[data.key]"
        />
        <div class="flex h-14 w-full justify-center">
          <select
            required
            class="bg-[#1A1919] h-9 w-1/2 border-2 border-gray-600 rounded-lg mx-1"
            id="program_id"
            v-model="formData.program"
          >
            <option
              v-for="program in programs"
              :key="program.value"
              :value="program.value"
            >
              {{ program.text }}
            </option>
          </select>

          <select
            required
            class="bg-[#1A1919] h-9 w-1/2 border-2 border-gray-600 rounded-lg mx-1"
            id="year_level"
            v-model="formData.year_level"
          >
            <option
              v-for="year in year_level"
              :key="year.value"
              :value="year.value"
            >
              {{ year.text }}
            </option>
          </select>
        </div>
        <div
          class="flex flex-col-reverse h-16 w-full justify-around items-center"
        >
          <NuxtLink to="/login"> Already have an account? </NuxtLink>
          <button
            class="h-12 w-72 bg-green-500 rounded-xl self-center text-xl"
            @click="submitForm"
            type="submit"
          >
            Register
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
const formData = ref({
  first_name: "",
  last_name: "",
  student_id: "",
  email: "",
  password: "",
  confirm_password: "",
  program: "",
  year_level: "",
});

const student = [
  { id: "first_name", placeholder: "First Name", key: "first_name" },
  { id: "last_name", placeholder: "Last Name", key: "last_name" },
  { id: "student_id", placeholder: "Student ID", key: "student_id" },
  { id: "email", placeholder: "Email", key: "email" },
  { id: "password", placeholder: "Password", key: "password" },
  {
    id: "confirm_password",
    placeholder: "Confirm Password",
    key: "confirm_password",
  },
];

const programs = [
  { value: "1", text: "BSIT" },
  { value: "2", text: "BSCS" },
  { value: "3", text: "BSIS" },
];
const year_level = [
  { value: "1", text: "First Year" },
  { value: "2", text: "Second Year" },
  { value: "3", text: "Third Year" },
  { value: "4", text: "Fourth Year" },
  { value: "5", text: "Fifth Year" },
];

// const getCSRFToken = () => {
//   const csrfToken = document.cookie
//     .split("; ")
//     .find((row) => row.startsWith("XSRF-TOKEN="));
//   return csrfToken ? decodeURIComponent(csrfToken.split("=")[1]) : null;
// };
const submitForm = async () => {
  event.preventDefault();
  // const csrfToken = getCSRFToken();

  // if (!csrfToken) {
  //   console.error("CSRF token not found.");
  //   return;
  // }
  if (formData.value.password !== formData.value.confirm_password) {
    alert("Passwords do not match!");
    return;
  } else {
    try {
      const { data } = await useFetch(
        "https://wtf-backend-production.up.railway.app/api/auth/register",
        {
          method: "POST",
          body: {
            first_name: formData.value.first_name,
            last_name: formData.value.last_name,
            student_id: formData.value.student_id,
            email: formData.value.email,
            password: formData.value.password,
            program_id: formData.value.program,
            year_level_code: formData.value.year_level,
          },
        }
      );
      if (error.value) {
        console.error("Registration failed:", error.value);
      } else {
        console.log("Registration successful:", data.value);
        $router.push("/login");
      }
    } catch (error) {
      alert("An error occurred during registration. Please try again.");
      console.error("Registration error:", error);
    }

    console.log(formData.value);
  }
};
</script>
