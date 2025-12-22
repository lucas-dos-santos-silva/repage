<script setup>
import {ref} from "vue";
import {Button} from "primevue";
const exampleImages = [
  "https://picsum.photos/200/300",
  "https://picsum.photos/200/300",
  "https://picsum.photos/200/300",
  "https://picsum.photos/200/300",
  "https://picsum.photos/200/300",
]

const fileInput = ref(null);
const imageUrl = ref(null);

const selectImage = () => {
    fileInput.value.click();
}

const onFileSelected = (e) => {
  fileInput.value = e.target.files[0];
  const file = e.target.files[0];
  if (file) {
    imageUrl.value = URL.createObjectURL(file);
  }
}

</script>

<template>
  <div class="h-16 bg-neutral-700 shadow-sm shadow-neutral-700 content-center">
    <h1 class="text-center">AppBar</h1>
  </div>
  <div class="px-5 pt-5 sm:px-20 sm:pt-20">
    <div class="pb-3 dark:text-white">
      <h1 class="text-lg">Comece com uma foto</h1>
      <p class="text-sm dark">Adicione uma imagem ou selecione um template</p>
    </div>
    <div v-if="imageUrl == null"
        class="flex h-[45vh] justify-center items-center dark:bg-neutral-800 border-2 border-dashed border-gray-200 rounded-2xl mb-5">
      <div @click="selectImage" class="flex items-center px-4 gap-3 py-2 dark:bg-white rounded-3xl dark:hover:bg-neutral-600 transition duration-300 ease-in-out cursor-pointer">
        <p class="text-black text-xl font-google-sans-flex">Adicionar Foto</p>

        <div class="w-8 h-8 rounded-full dark:bg-black flex items-center justify-center">
          <span class="pi pi-plus dark:text-white text-sm"></span>
        </div>

      </div>
      <input type="file" ref="fileInput" class="hidden" @change="onFileSelected">
    </div>
    <div v-else>
      <div
          :style="{ backgroundImage: `url(${imageUrl})` }"
          class="h-[45vh] w-full rounded-2xl mb-5 bg-center bg-no-repeat bg-contain dark:bg-neutral-800"
      >
      </div>
    </div>
    <div class="flex pt-3 overflow-x-auto gap-3 h-56">
      <img v-for="(item, index) in exampleImages" :key="index" :src="item" alt="" class="rounded-3xl hover:scale-[1.05] transition duration-300 ease-in-out">
    </div>
    <div class="pt-5">
      <button class="w-full p-3 rounded-3xl bg-white dark:hover:bg-neutral-600 transition duration-300 ease-in-out">
        <p class="text-2xl text-black font-medium">Próximo</p>
      </button>
    </div>
  </div>
</template>
<style>
</style>
