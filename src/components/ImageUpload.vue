<script setup lang="ts">
    import {ref} from "vue";

    const emits = defineEmits(['file-selected']);
    const fileInput = ref(null);

    const selectImage = () => {
      fileInput.value.click();
    }

    const onFileSelected = (e) => {
      fileInput.value = e.target.files[0];
      const file = e.target.files[0];

      if (file) {
        emits('file-selected', file);
      }
    }

</script>

<template>
  <div class="flex h-[30vh] justify-center items-center border-2 border-dashed border-gray-200 rounded-4xl mb-5">
    <div @click="selectImage"
         class="flex items-center px-4 gap-3 py-2 dark:bg-white rounded-3xl dark:hover:bg-neutral-600 transition duration-300 ease-in-out cursor-pointer">

      <p class="text-black text-xl font-google-sans-flex">Adicionar Foto</p>

      <div class="w-8 h-8 rounded-full dark:bg-black flex items-center justify-center">
        <span class="pi pi-plus dark:text-white text-sm"></span>
      </div>

    </div>
    <input type="file" ref="fileInput" @change="onFileSelected" class="hidden"/>
  </div>
</template>

<style scoped>

</style>