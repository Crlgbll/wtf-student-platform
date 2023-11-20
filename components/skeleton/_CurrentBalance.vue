<template>
  <div
    class="gap-5 flex flex-col h-40 w-[350px] bg-[#1F6562] rounded-2xl border-gray-500 border-2 p-3 animate-pulse"
  >
    <div class="flex h-[138px] w-full flex-col relative justify-end gap-3">
      <div class="h-10 w-7 rounded-full bg-slate-100"></div>
      <h1 class="text-base">Your Current Balance</h1>
      <div class="h-16 w-60 bg-[#535252] rounded-full"></div>
      <div class="h-8 w-10 bg-[#535252] rounded-full"></div>

      <img
        class="absolute right-0 bottom-0"
        src="~/assets/images/circles.png"
        alt=""
      />
    </div>
  </div>
</template>

<script>
export default {
  async created() {
    await this.studentTotalPaid();
    this.updateTime();
    // Update time every second (1000 milliseconds)
    setInterval(this.updateTime, 1000);
  },
  method: {
    updateTime() {
      const now = new Date();

      // Options for formatting date and time
      const dateFormatOptions = {
        year: "numeric",
        month: "long",
        day: "numeric",
      };

      const timeFormatOptions = {
        hour: "2-digit",
        minute: "2-digit",
        second: "2-digit",
        timeZoneName: "short",
      };

      // Set current date
      this.currentDate = now.toLocaleDateString(undefined, dateFormatOptions);

      // Set current time
      this.currentTime = now.toLocaleTimeString(undefined, timeFormatOptions);
    },
  },
};
</script>

<style lang="scss" scoped></style>
