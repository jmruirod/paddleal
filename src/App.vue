<script setup lang="ts">
import { ref, onMounted, watch } from "vue";
import PaddleCard from "./components/PaddleCard.vue";
import HeaderComponent from "./components/HeaderComponent.vue";
import FooterComponent from "./components/FooterComponent.vue";
import { db } from "./data/paddles";
import type { Paddle } from "./model/Paddle";
import type { CartItem } from "./model/CartItem";
import Swal from "sweetalert2";

const paddles = ref<Paddle[]>([] as Paddle[]);
const headerPaddle = ref<Paddle>({} as Paddle);
const cart = ref<CartItem[]>([] as CartItem[]);

watch(
  cart,
  () => {
    saveLocalStorage();
  },
  { deep: true },
);

onMounted(() => {
  paddles.value = db;
  headerPaddle.value = paddles.value[2];

  const cartFromLocalStorage = localStorage.getItem("cart");
  if (cartFromLocalStorage) {
    cart.value = JSON.parse(cartFromLocalStorage);
  }
});

const saveLocalStorage = () => {
  localStorage.setItem("cart", JSON.stringify(cart.value));
};

const addToCart = (paddle: Paddle) => {
  const paddleInCartIndex = cart.value.findIndex((cart) => cart.id === paddle.id);
  if (paddleInCartIndex === -1) {
    cart.value.push({ id: paddle.id, name: paddle.name, description: paddle.description, price: paddle.price, image: paddle.image, quantity: 1 });
  } else {
    cart.value[paddleInCartIndex].quantity += 1;
  }

  Swal.fire({
    title: "Producto agregado al carrito",
    icon: "success",
    showConfirmButton: false,
    toast: true,
    position: "top-right",
    timer: 1500,
  });
};

const decreaseQuantity = (id: number) => {
  const paddleInCartIndex = cart.value.findIndex((cart) => cart.id === id);
  if (cart.value[paddleInCartIndex].quantity === 1) {
    cart.value = cart.value.filter((cart) => cart.id !== id);
  } else {
    cart.value[paddleInCartIndex].quantity -= 1;
  }
};

const increaseQuantity = (id: number) => {
  const paddleInCartIndex = cart.value.findIndex((cart) => cart.id === id);
  if (cart.value[paddleInCartIndex].quantity >= 99) {
    return;
  }
  cart.value[paddleInCartIndex].quantity += 1;
};

const removeFromCart = (id: number) => {
  Swal.fire({
    title: "¿Quieres eliminar este producto?",
    icon: "question",
    showCancelButton: true,
    cancelButtonText: "Cancelar",
    confirmButtonText: "Eliminar",
    confirmButtonColor: "oklch(75% 0.183 55.934)",
  }).then((result) => {
    if (result.isConfirmed) {
      cart.value = cart.value.filter((cart) => cart.id !== id);
    }
  });
};

const clearCart = () => {
  Swal.fire({
    title: "¿Quieres vaciar el carrito?",
    icon: "question",
    showCancelButton: true,
    cancelButtonText: "Cancelar",
    confirmButtonText: "Vaciar",
    confirmButtonColor: "oklch(75% 0.183 55.934)",
  }).then((result) => {
    if (result.isConfirmed) {
      cart.value = [];
    }
  });
};

const isCartOpen = ref(false);

const toggleCart = () => {
  if (window.matchMedia("(hover: hover)").matches) {
    return;
  }

  isCartOpen.value = !isCartOpen.value;
};

const closeCart = (event?: MouseEvent) => {
  if (window.matchMedia("(hover: hover)").matches) {
    return;
  }

  const target = event?.target as HTMLElement;
  const isCartClicked = target.closest('[alt="imagen carrito"]') !== null;

  if (isCartOpen.value && !isCartClicked) {
    isCartOpen.value = false;
  }
};
</script>

<template>
  <div class="flex flex-col items-center" @click="closeCart($event)">
    <HeaderComponent
      :header-paddle="headerPaddle!"
      :cart="cart"
      :is-cart-open="isCartOpen"
      @remove-from-cart="removeFromCart"
      @decrease-quantity="decreaseQuantity"
      @increase-quantity="increaseQuantity"
      @add-to-cart="addToCart"
      @clear-cart="clearCart"
      @toggle-cart="toggleCart"
      @close-cart="closeCart($event)"
    />

    <main class="max-w-[1536px]">
      <div class="flex items-center justify-center min-h-[150px]">
        <h2 class="text-4xl md:text-6xl font-black text-rose-500">Nuestra Colección</h2>
      </div>

      <div class="mt-2 grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-x-4 gap-y-8">
        <PaddleCard v-for="paddle in paddles" :key="paddle.id" :paddle="paddle" @add-to-cart="addToCart" />
      </div>
    </main>

    <FooterComponent />
  </div>
</template>

<style scoped>
.bg-header {
  background: linear-gradient(to right, rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), url(/img/header.jpg);
  background-size: cover;
  background-position: center;
}

@keyframes guitar-animation {
  0% {
    opacity: 0;
    transform: translateX(-10rem);
  }
  50% {
    opacity: 0;
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

.header-guitar {
  animation: guitar-animation 1s ease-in-out;
}
</style>
