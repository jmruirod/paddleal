<script setup lang="ts">
import type { PropType } from "vue";
import ShoppingCartItem from "./ShoppingCartItem.vue";
import { computed } from "vue";

const props = defineProps({
  cart: {
    type: Array as PropType<
      {
        id: number;
        name: string;
        description: string;
        price: number;
        image: string;
        quantity: number;
      }[]
    >,
    required: true,
  },
  headerPaddle: {
    type: Object as PropType<{ id: number; name: string; description: string; price: number; image: string }>,
    required: true,
  },
  isCartOpen: {
    type: Boolean,
    required: true,
  },
});

const emit = defineEmits(["remove-from-cart", "decrease-quantity", "increase-quantity", "add-to-cart", "clear-cart", "toggle-cart", "close-cart"]);

const removeFromCart = (id: number) => {
  emit("remove-from-cart", id);
};

const decreaseQuantity = (id: number) => {
  emit("decrease-quantity", id);
};

const increaseQuantity = (id: number) => {
  emit("increase-quantity", id);
};

const totalPrice = computed(() => {
  return props.cart.reduce((total, cartItem) => total + cartItem.price * cartItem.quantity, 0);
});

const toggleCart = () => {
  if (window.matchMedia("(hover: hover)").matches) {
    return;
  }

  emit("toggle-cart");
};

const closeCart = (event: MouseEvent) => {
  if (window.matchMedia("(hover: hover)").matches) {
    return;
  }

  emit("close-cart", event as MouseEvent);
};
</script>

<template>
  <header class="relative py-10 w-full flex justify-center bg-header">
    <div class="w-full max-w-[95%] lg:max-w-[80%] flex flex-col justify-between min-h-[75vh]">
      <div class="flex flex-col lg:flex-row justify-start items-center lg:justify-between lg:items-end gap-y-8">
        <a href="/">
          <div class="flex justify-center md:justify-start">
            <div class="flex items-center justify-center">
              <img src="/paddleal/img/padelIcon128.png" alt="icono padel" class="-ml-10" />
            </div>
            <div class="-ml-9">
              <p class="text-white text-7xl font-bold">Padel<span class="text-pink-600 font-black">AL</span></p>
              <p class="text-white text-xl font-bold">PALAS - CURSOS - TORNEOS</p>
            </div>
          </div>
        </a>

        <nav class="self-end flex items-start justify-end">
          <div class="relative max-w-[3rem] hover:[&>div]:flex z-1" @click.stop>
            <img
              class="max-w-full h-auto"
              :class="{ 'scale-90 transition-all': isCartOpen }"
              src="/paddleal/img/basket.png"
              alt="imagen carrito"
              @click="toggleCart()"
            />

            <div class="p-4 hidden hover:block absolute top-8 -right-3" :class="{ '!flex': isCartOpen }" @click="closeCart($event)">
              <div class="bg-white p-4 w-[355px] sm:w-xl flex flex-col gap-2 shadow-lg rounded-md" @click.stop>
                <p v-if="cart.length === 0" class="text-center py-2 text-zinc-600">El carrito esta vacio</p>
                <div v-else>
                  <ShoppingCartItem
                    v-for="cartItem in cart"
                    :key="cartItem.id"
                    :cartItem="cartItem"
                    @remove-from-cart="removeFromCart"
                    @decrease-quantity="decreaseQuantity"
                    @increase-quantity="increaseQuantity"
                  />

                  <p class="text-end text-base sm:text-xl py-2">
                    Total pagar: <span class="font-bold">{{ totalPrice.toFixed(2) }}€</span>
                  </p>
                  <button
                    class="mt-5 w-full bg-zinc-700 hover:bg-zinc-600 active:bg-zinc-700 text-white uppercase font-black py-2 px-4 rounded-md active:scale-95 transition-all duration-300"
                    @click="emit('clear-cart')"
                  >
                    Vaciar Carrito
                  </button>
                </div>
              </div>
            </div>
          </div>
        </nav>
      </div>

      <div class="flex flex-col gap-y-10 w-full lg:w-[50%] items-center lg:items-start">
        <h1 class="text-5xl lg:text-7xl text-center lg:text-left font-bold text-pink-600">{{ headerPaddle.name }}</h1>
        <p class="mt-5 text-white text-center lg:text-left text-xl">
          {{ headerPaddle.description }}
        </p>
        <div class="flex flex-col items-center lg:items-start gap-y-3">
          <p class="mt-5 text-7xl font-bold text-pink-600">{{ headerPaddle.price }}€</p>
          <button
            type="button"
            class="mt-5 text-2xl bg-pink-600 hover:bg-pink-500 active:bg-pink-600 text-white font-black py-2 px-5 rounded-md active:scale-95 transition-all duration-300"
            @click="emit('add-to-cart', headerPaddle)"
          >
            Agregar al Carrito
          </button>
        </div>
      </div>
    </div>

    <img class="header-guitar hidden xl:block absolute bottom-0 right-0" src="/img/headerPaddle.png" alt="imagen header" />
  </header>
</template>
