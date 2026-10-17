<script setup>
import { useFavoritesStore } from "@/stores/favorites";
import { useCartStore } from "@/stores/cart";

const favoritesStore = useFavoritesStore();
const cartStore = useCartStore();

defineProps({
  product: Object,
});
</script>

<template>
  <div class="p-5 bg-slate-100 rounded-4xl flex items-start justify-between gap-10">
    <div class="flex gap-4 flex-1">
      <div class="w-30 h-30 overflow-hidden">
        <img :src="product.imageUrl" alt="" class="w-full h-full object-cover" />
      </div>
      <div class="pt-2">
        <h3 class="text-xl font-semibold mb-3">{{ product.title }}</h3>
        <div class="flex gap-3 items-center">
          <button
            @click="favoritesStore.toggleFavorite(product)"
            class="rounded-4xl bg-white shadow p-3 cursor-pointer hover:scale-110 transition"
          >
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M9.99999 18.0417C9.74166 18.0417 9.49166 18.0083 9.28332 17.9333C6.09999 16.8417 1.04166 12.9667 1.04166 7.58332C1.04166 4.39166 3.62499 1.79166 6.79166 1.79166C8.11666 1.79166 9.38332 2.24166 10 3.06666C10.6167 2.24166 11.8833 1.79166 13.2083 1.79166C16.375 1.79166 18.9583 4.39166 18.9583 7.58332C18.9583 12.9667 13.9 16.8417 10.7167 17.9333C10.5083 18.0083 10.2583 18.0417 9.99999 18.0417Z" fill="#263141" />
            </svg>
          </button>
          <button
            @click="cartStore.removeFromCart(product.id)"
            class="rounded-4xl bg-white shadow p-3 cursor-pointer hover:scale-110 transition"
          >
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M18 5.31667C15.225 5.04167 12.4333 4.9 9.65 4.9C8 4.9 6.35 4.98333 4.7 5.15L3 5.31667M7.58333 4.475L7.76667 3.39167C7.9 2.6 8 2 9.40833 2H10.5917C12 2 12.1083 2.63333 12.2333 3.4L12.4167 4.475M16.5 7.39167L15.8333 17.725C15.7417 19.1417 15.6667 20 13.15 20H6.85C4.33333 20 4.25833 19.1417 4.16667 17.725L3.5 7.39167M8.33333 15H11.6667M7.5 11.25H12.5" stroke="#263141" stroke-width="1.25" stroke-linecap="round" stroke-linejoin="round" />
            </svg>
          </button>
        </div>
      </div>
    </div>
    <div class="pt-2">
      <b class="text-xl">{{ product.price.toLocaleString("ru-RU") }} ₽</b>
    </div>
    <div class="rounded-4xl bg-white p-1 flex items-center">
      <button
        @click="cartStore.updateQuantity(product.id, -1)"
        class="cursor-pointer w-10 h-10 font-bold flex items-center justify-center rounded-4xl p-3 hover:bg-slate-200 transition"
      >
        -
      </button>
      <span class="w-12 text-center">{{ product.quantity }}</span>
      <button
        @click="cartStore.updateQuantity(product.id, 1)"
        class="cursor-pointer w-10 h-10 font-bold flex items-center justify-center rounded-4xl p-3 hover:bg-slate-200 transition"
      >
        +
      </button>
    </div>
  </div>
</template>

<style scoped></style>
