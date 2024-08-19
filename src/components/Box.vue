<script setup lang="ts">
import { ref, onMounted } from "vue";
import On from "on-dom";

const overlay = ref(false);
const handleOverlay = () => (overlay.value = false);

const redirect = ref("");
// const pointer = <{ x: number; y: number }>ref({ x: 0, y: 0 });

const linkItems = ref([
  { link: "https://github.com/nonso01", text: "Github" },
  {
    link: "chukwunonsomartin01@gmail.com",
    text: "Gmail",
  },
  {
    link: "https://www.linkedin.com/in/nonso-martin-80b221238",
    text: "LinkedIn",
  },
  { link: "https://x.com/nonso0X", text: "Twitter" },
  { link: "https://nonso01.vercel.app", text: "Portfolio" },
]);

onMounted(() => {
   new On("div[data-link]", {
    click() {
      redirect.value = this?.dataset.link;
      overlay.value = true;
    },
  });
});
</script>

<template>
  <div
    class="p-[5%] sm:p-[2%] bg-dark-grey w-[18.75rem] sm:w-[22rem] h-[34.375rem] flex flex-col justify-between rounded-lg"
  >
    <div class="flex flex-col justify-evenly items-center h-[30%]">
      <!-- for the hero image and details -->
      <img
        src="../svrou0.jpg"
        alt="nonso martin"
        class="w-16 h-16 rounded-full transition-colors outline outline-offset-4 outline-dark-grey hover:outline-green"
      />
      <h3 class="text-white text-xl font-semibold font-sans">Nonso Martin</h3>
      <p class="text-green font-sans font-semibold text-xs">Enugu , Nigeria</p>
    </div>
    <!-- -->
    <div>
      <p class="text-white text-xs font-sans text-center">
        "Front-end developer and Medical Scientist"
      </p>
    </div>

    <!---->
    <div class="flex flex-col justify-between h-[60%]">
      <div
        v-for="{ link, text } in linkItems"
        :data-link="link"
        class="text-white font-semibold text-xs bg-grey h-12 flex flex-col items-center justify-center rounded-md transition-colors hover:bg-green hover:text-off-black"
      >
        {{ text }}
      </div>
    </div>
  </div>

  <template v-if="overlay">
    <!-- would have used Transition -->
    <div
      class="h-dvh w-dvw fixed transition-colors"
      data-overlay="o"
      @click="handleOverlay"
    ></div>
    <div
      class="w-60 h-40 rounded-md bg-grey fixed flex flex-col justify-evenly items-center"
      data-dialog="o"
    >
      <p class="text-white text-xs font-medium">
        You'll be redirected to a different page!
      </p>
      <button
        class="rounded-md bg-green text-off-black text-xs font-semibold w-[70%] h-10"
      >
        <a _target="blank" :href="redirect">Take me away!</a>
      </button>
    </div>
  </template>
</template>
