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
    <div
        class="p-5 bg-slate-100 rounded-xl flex flex-col justify-between gap-2"
    >
        <div>
            <img
                :src="product.imgUrl"
                alt=""
                class="mb-4"
            />
            <h3 class="text-xl font-semibold">
                {{ product.title }}
            </h3>
        </div>
        <div class="flex items-center justify-between gap-2">
            <div>
                <p class="text-slate-500">Цена</p>
                <b class="text-xl"
                    >{{ product.price.toLocaleString("ru-RU") }} ₽</b
                >
            </div>
            <div class="flex items-center gap-3">
                <button
                    @click="favoritesStore.toggleFavorite(product)"
                    class="rounded-4xl shadow p-3 cursor-pointer hover:scale-110 transition"
                    :class="[
                        favoritesStore.isFavorite(product.id)
                            ? 'bg-red-500 '
                            : 'bg-white',
                    ]"
                >
                    <svg
                        width="20"
                        height="20"
                        viewBox="0 0 20 20"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            d="M9.99999 18.0417C9.74166 18.0417 9.49166 18.0083 9.25833 17.9417C6.44166 17.1333 2.08333 13.275 2.08333 8.54166C2.08333 5.23333 4.60833 2.5 7.70833 2.5C8.95833 2.5 10.15 3.025 11.05 3.95833C11.3417 4.25833 11.5917 4.6 11.7917 4.96666C11.9917 4.6 12.2417 4.25833 12.5333 3.95833C13.4333 3.025 14.625 2.5 15.875 2.5C18.975 2.5 21.5 5.23333 21.5 8.54166C21.5 13.275 17.1417 17.1333 14.325 17.9417C14.0917 18.0083 13.8417 18.0417 13.5833 18.0417H9.99999Z"
                            :fill="favoritesStore.isFavorite(product.id) ? '#fff' : '#263141'"
                        />
                    </svg>
                </button>
                <button
                    @click="cartStore.isAdded(product.id) ? cartStore.removeFromCart(product.id) : cartStore.addToCart(product)"
                    class="rounded-4xl shadow p-3 cursor-pointer hover:scale-110 transition"
                    :class="[cartStore.isAdded(product.id) ? 'bg-red-500' : 'bg-white']"
                >
                    <svg
                        width="20"
                        height="20"
                        viewBox="0 0 20 20"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path v-show="cartStore.isAdded(product.id)"
                            d="M18 5.31667C15.225 5.04167 12.4333 4.9 9.65 4.9C8 4.9 6.35 4.98333 4.7 5.15L3 5.31667M7.58333 4.475L7.76667 3.38333C7.9 2.59167 8 2 9.40833 2H11.5917C13 2 13.1083 2.625 13.2333 3.39167L13.4167 4.475M16.2083 7.95L15.6667 16.3417C15.575 17.65 15.5 18.6667 13.175 18.6667H7.825C5.5 18.6667 5.425 17.65 5.33333 16.3417L4.79167 7.95M9.10833 14.0833H11.8833M8.41667 10.75H12.5833" stroke="white" stroke-width="1.25" stroke-linecap="round" stroke-linejoin="round"/>
                        <path
                            v-show="!cartStore.isAdded(product.id)"
                            d="M4.16666 5.83333H15.6583C15.8912 5.83334 16.1214 5.88214 16.3343 5.97659C16.5471 6.07103 16.7378 6.20903 16.894 6.38168C17.0503 6.55433 17.1686 6.7578 17.2414 6.97898C17.3142 7.20016 17.3398 7.43414 17.3167 7.66583L16.8167 12.6658C16.7755 13.0771 16.5831 13.4584 16.2766 13.7357C15.9702 14.0131 15.5716 14.1667 15.1583 14.1667H7.19999C6.81455 14.1668 6.44097 14.0334 6.14286 13.789C5.84475 13.5447 5.64054 13.2046 5.56499 12.8267L4.16666 5.83333ZM4.16666 5.83333L3.49166 3.13083C3.44651 2.95063 3.34245 2.79067 3.196 2.67638C3.04954 2.56209 2.8691 2.5 2.68332 2.5H1.66666M6.66666 17.5H8.33332M13.3333 17.5H15" stroke="#263141" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"
                        />
                    </svg>
                </button>
            </div>
        </div>
    </div>
</template>