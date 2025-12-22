<script setup>
import {ref} from "vue";
import {Button} from "primevue";
import ImageUpload from "@/components/ImageUpload.vue";


const modulos = import.meta.glob('@/assets/testImages/*.{png,jpg,jpeg,svg}', { eager: true });

const exampleImages = Object.values(modulos).map((mod) => mod.default);

const imageUrl = ref(null);
const isFileSelected = ref(null);

const handleFile = (file) => {
  isFileSelected.value = true;
  imageUrl.value = URL.createObjectURL(file);
}

</script>

<template>
  <!-- AppBar -->
  <div class="h-16 bg-neutral-900 shadow-sm shadow-neutral-800 content-center">
    <h1 class="text-center">YourApp</h1>
  </div>
  <!-- Main content -->
  <main class="px-5 pt-5 sm:px-20 sm:pt-20">
    <!-- Title and description -->
    <div class="pb-3 dark:text-white">
      <h1 class="text-lg">Comece com uma foto</h1>
      <p class="text-sm dark">Adicione uma imagem ou selecione um template</p>
    </div>
    <!-- Image upload area -->

    <ImageUpload
        v-if="!isFileSelected"
        @file-selected="handleFile"
    />

    <img v-else :src="imageUrl" alt="" class="rounded-2xl mb-5 mt-5 bg-center lg:w-1/3 justify-self-center">
    <!-- Example images carousel -->
    <div v-if="!isFileSelected" class="flex pt-3 overflow-x-auto gap-3">
      <img v-for="(item, index) in exampleImages" :key="index" :src="item" alt=""
           class="rounded-3xl hover:scale-[1.05] transition duration-300 ease-in-out w-2/6">
    </div>
    <!-- Next button -->
    <div class="pt-5 h-full items-center">
      <button :disabled="!isFileSelected" class="w-full p-3 rounded-3xl bg-white dark:hover:bg-neutral-600 transition duration-300 ease-in-out"
              :class="!isFileSelected ? 'cursor-not-allowed opacity-50' : 'cursor-pointer'" >
        <p class="text-2xl text-black font-medium">Próximo</p>
      </button>
    </div>
  </main>
</template>
<style>
</style>
