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
  <div class="p-5 bg-slate-100 rounded-xl flex flex-col justify-between gap-2">
    <div>
      <img :src="product.imageUrl" alt="" class="mb-4" />
      <h3 class="text-xl font-semibold">{{ product.title }}</h3>
    </div>

    <div class="flex items-center justify-between gap-2">
      <div>
        <p class="text-slate-500">Цена</p>
        <b class="text-xl">{{ product.price.toLocaleString("ru-RU") }} ₽</b>
      </div>

      <div class="flex items-center gap-3">
        <button
          @click="favoritesStore.toggleFavorite(product)"
          class="rounded-4xl shadow p-3 cursor-pointer hover:scale-110 transition"
          :class="[favoritesStore.isFavorite(product.id) ? 'bg-red-500' : 'bg-white']"
        >
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path
              d="M9.99999 18.0417C9.74166 18.0417 9.49166 18.0083 9.28332 17.9333C6.09999 16.8417 1.04166 12.9667 1.04166 7.58332C1.04166 4.39166 3.62499 1.79166 6.79166 1.79166C8.11666 1.79166 9.38332 2.24166 10 3.06666C10.6167 2.24166 11.8833 1.79166 13.2083 1.79166C16.375 1.79166 18.9583 4.39166 18.9583 7.58332C18.9583 12.9667 13.9 16.8417 10.7167 17.9333C10.5083 18.0083 10.2583 18.0417 9.99999 18.0417Z"
              :fill="favoritesStore.isFavorite(product.id) ? '#fff' : '#263141'"
            />
          </svg>
        </button>

        <button
          @click="cartStore.isAdded(product.id) ? cartStore.removeFromCart(product.id) : cartStore.addToCart(product)"
          class="rounded-4xl shadow p-3 cursor-pointer hover:scale-110 transition"
          :class="[cartStore.isAdded(product.id) ? 'bg-red-500' : 'bg-white']"
        >
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path
              v-show="cartStore.isAdded(product.id)"
              d="M18 5.31667C15.225 5.04167 12.4333 4.9 9.65 4.9C8 4.9 6.35 4.98333 4.7 5.15L3 5.31667M7.58333 4.475L7.76667 3.39167C7.9 2.6 8 2 9.40833 2H10.5917C12 2 12.1083 2.63333 12.2333 3.4L12.4167 4.475M16.5 7.39167L15.8333 17.725C15.7417 19.1417 15.6667 20 13.15 20H6.85C4.33333 20 4.25833 19.1417 4.16667 17.725L3.5 7.39167M8.33333 15H11.6667M7.5 11.25H12.5"
              stroke="white"
              stroke-width="1.25"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <path
              v-show="!cartStore.isAdded(product.id)"
              d="M4.16666 5.83333H15.6583C15.8917 5.83333 16.1217 5.88333 16.3342 5.98166C16.5467 6.08 16.7342 6.22333 16.8842 6.40166C17.0342 6.58 17.1417 6.78833 17.1992 7.015C17.2567 7.24166 17.2617 7.47833 17.2142 7.70833L16.0725 13.2083C15.9392 13.8517 15.5725 14.4233 15.0392 14.8183C14.5058 15.2133 13.8458 15.405 13.1808 15.3583H6.81916C6.15416 15.405 5.49416 15.2133 4.96083 14.8183C4.4275 14.4233 4.06083 13.8517 3.9275 13.2083L2.6175 4.39166C2.56333 4.025 2.38166 3.69166 2.10666 3.45C1.83166 3.20833 1.48333 3.07666 1.12416 3.08083H0.83333"
              stroke="#263141"
              stroke-width="1.5"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
