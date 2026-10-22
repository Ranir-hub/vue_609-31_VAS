<script setup>
import { useFavoritesStore } from '@/stores/favorites';
import { useCartStore } from "@/stores/cart"

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
                <img :src="product.imgUrl"
                    alt=""
                    class="w-full h-full object-cover"/> 
            </div>
            <div class="pt-2">
                <h3 class="text-xl font-semibold mb-3">
                    {{ product.title }}
                </h3>
                <div class="flex gap-3 items-center">
                    <button @click="favoritesStore.toggleFavorite(product)"
                            class="rounded-4xl bg-white shadow p-3 cursor-pointer hover:scale-110 transition">
                        <svg
                            width="20"
                            height="20"
                            viewBox="0 0 20 20"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg">
                            <path
                                d="M9.99999 18.0417C9.74166 18.0417 9.49166 18.0083 9.25833 17.9417C6.44166 17.1333 2.08333 13.275 2.08333 8.54166C2.08333 5.23333 4.60833 2.5 7.70833 2.5C8.95833 2.5 10.15 3.025 11.05 3.95833C11.3417 4.25833 11.5917 4.6 11.7917 4.96666C11.9917 4.6 12.2417 4.25833 12.5333 3.95833C13.4333 3.025 14.625 2.5 15.875 2.5C18.975 2.5 21.5 5.23333 21.5 8.54166C21.5 13.275 17.1417 17.1333 14.325 17.9417C14.0917 18.0083 13.8417 18.0417 13.5833 18.0417H9.99999Z"
                                fill="#263141"/>
                        </svg>    
                    </button>
                    <button
                        @click="cartStore.removeFromCart(product.id)"
                        class="rounded-4xl bg-white shadow p-3 cursor-pointer hover:scale-110 transition">
                        <svg
                            width="20"
                            height="20"
                            viewBox="0 0 20 20"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg">
                            <path
                                d="M18 5.31667C15.225 5.04167 12.4333 4.9 9.65 4.9C8 4.9 6.35 4.98333 4.7 5.15L3 5.31667M7.58333 5.31667V3.81667C7.58333 2.99167 8.25 2.31667 9.08333 2.31667H10.9167C11.75 2.31667 12.4167 2.99167 12.4167 3.81667V5.31667M15.5 5.31667L15.1667 16.15C15.1417 16.9417 14.5083 17.575 13.725 17.575H6.275C5.49167 17.575 4.85833 16.9417 4.83333 16.15L4.5 5.31667"
                                stroke="#263141"
                                stroke-width="1.25"
                                stroke-linecap="round"
                                stroke-linejoin="round"/>
                        </svg>  
                    </button>
                </div>
            </div>
        </div>
        <div class="pt-2">
            <b class="text-xl">{{ product.price.toLocaleString("ru-RU") }} ₽</b>
        </div>
        <div class="rounded-4xl bg-white p-1 flex items-center">
            <button class="cursor-pointer w-10 h-10 font-bold flex items-center justify-center rounded-4xl p-3 hover:bg-slate-200 transition"
                    @click="cartStore.updateQuantity(product.id, -1)">
                -
            </button>
            <span class="w-12 text-center">{{ product.quantity }}</span>
            <button class="cursor-pointer w-10 h-10 font-bold flex items-center justify-center rounded-4xl p-3 hover:bg-slate-200 transition"
                    @click="cartStore.updateQuantity(product.id, 1)">
                +    
            </button>
        </div>
    </div>
</template>