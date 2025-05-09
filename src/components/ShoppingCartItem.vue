<script setup lang="ts">
defineProps<{
  cartItem: {
    id: number;
    name: string;
    description: string;
    price: number;
    image: string;
    quantity: number;
  };
}>();
const emit = defineEmits(["remove-from-cart", "decrease-quantity", "increase-quantity"]);
</script>

<template>
  <div class="grid grid-cols-[minmax(0,1fr)_minmax(0,2fr)_minmax(0,1fr)] grid-rows-2">
    <img class="w-full h-auto row-span-2" :src="`/paddleal/img/${cartItem.image}.jpg`" :alt="cartItem.name" />

    <div class="text-base sm:text-xl">{{ cartItem.name }}</div>

    <div class="justify-self-end self-center">
      <button @click="emit('remove-from-cart', cartItem.id)" class="hover:opacity-80 active:scale-85 transition-all duration-300" type="button">
        <img src="/img/trash.png" alt="icono eliminar" class="size-6 sm:size-8" />
      </button>
    </div>

    <div class="font-bold text-base sm:text-3xl self-end">{{ `${cartItem.price} €` }}</div>

    <div class="flex justify-center items-center gap-3 justify-self-center self-end text-base sm:text-xl">
      <button
        type="button"
        class="bg-zinc-700 hover:bg-zinc-600 active:bg-zinc-700 text-white font-black px-3 sm:px-4 rounded-md active:scale-95 transition-all duration-300"
        @click="emit('decrease-quantity', cartItem.id)"
      >
        -
      </button>
      <span>{{ cartItem.quantity }}</span>
      <button
        type="button"
        class="bg-zinc-700 hover:bg-zinc-600 active:bg-zinc-700 text-white font-black px-3 sm:px-4 rounded-md active:scale-95 transition-all duration-300"
        @click="emit('increase-quantity', cartItem.id)"
      >
        +
      </button>
    </div>
  </div>

  <div class="h-0.5 w-full bg-zinc-200 my-2"></div>
</template>
