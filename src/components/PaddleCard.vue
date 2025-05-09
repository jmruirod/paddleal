<script setup lang="ts">
defineProps<{
  paddle: {
    id: number;
    name: string;
    description: string;
    price: number;
    image: string;
  };
}>();
const emit = defineEmits(["add-to-cart"]);
</script>

<template>
  <div class="flex max-w-[500px] shadow-sm rounded-md p-4">
    <div class="w-full h-auto flex items-center">
      <img :src="`/img/${paddle.image}.jpg`" :alt="paddle.name" />
    </div>
    <div class="flex flex-col gap-3">
      <h3 class="uppercase text-sm xs:text-2xl font-bold">{{ paddle.name }}</h3>
      <p class="text-sm xs:text-base text-pretty line-clamp-3">{{ paddle.description }}</p>
      <p class="uppercase text-3xl xs:text-5xl font-black text-pink-600 mt-3">{{ `${paddle.price} €` }}</p>
      <button
        type="button"
        class="bg-zinc-700 hover:bg-zinc-600 active:bg-zinc-700 text-sm sm:text-base text-white uppercase font-black py-2 px-2 sm:px-4 rounded-md active:scale-95 transition-all duration-300"
        @click="emit('add-to-cart', paddle)"
      >
        Agregar al Carrito
      </button>
    </div>
  </div>
</template>
