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
  <main class="px-5 pt-5 sm:px-20 sm:pt-6">
    <!-- Title and description -->
    <div class="pb-3 dark:text-white lg:w-2/4 xl:w-8/12 lg:flex lg:justify-self-center">
      <div>
        <h1 class="text-lg">Comece com uma foto</h1>
        <p class="text-sm dark">Adicione uma imagem ou selecione um template</p>
      </div>
    </div>
    <!-- Image upload area -->

    <ImageUpload
        v-if="!isFileSelected"
        @file-selected="handleFile"
    />

    <div v-else class="flex justify-center mt-5">
      <div class="relative w-full lg:w-2/4 xl:w-8/12">
        <img :src="imageUrl" alt="Uploaded Image"
             class="rounded-2xl w-full h-auto max-h-[50vh] xl:max-h-[60vh] object-cover"/>
        <button type="button"
                class="pi pi-times absolute top-3 right-3 lg:top-4 lg:right-4 text-3xl cursor-pointer p-1 rounded-full bg-black/20 hover:bg-black/40"
                @click="isFileSelected = false; imageUrl = null"
                aria-label="Close">
        </button>
      </div>
    </div>
    <!-- Example images carousel -->
    <div v-if="!isFileSelected" class="flex p-3 overflow-x-auto gap-3 lg:h-[35vh]">
      <img v-for="(item, index) in exampleImages" :key="index" :src="item" alt=""
           class="rounded-3xl hover:scale-[1.05] transition duration-300 ease-in-out w-2/6 xl:1/6  cursor-pointer"/>
    </div>
    <!-- Next button -->
    <div class="pt-5 h-full items-center w-full flex justify-center">
      <button :disabled="!isFileSelected" class="w-80 text-center p-3 rounded-3xl bg-white dark:hover:bg-neutral-600 transition duration-300 ease-in-out"
              :class="!isFileSelected ? 'cursor-not-allowed opacity-50' : 'cursor-pointer'" >
        <p class="text-2xl text-black font-medium">Próximo</p>
      </button>
    </div>
  </main>
</template>
<style>
</style>
