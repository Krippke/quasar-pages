<template>
  <q-page class="row items-start q-pa-md">
    <div class="col-12">
      <h5 class="q-my-md">Products</h5>
    </div>
    <div v-for="product in products" :key="product.id" class="col-xs-12 col-sm-6 col-md-4 q-pa-sm">
      <q-card>
        <q-img :src="product.image" :ratio="1" />
        <q-card-section>
          <q-item-label class="text-subtitle1">{{ product.name }}</q-item-label>
          <q-item-label caption>Price: ${{ product.price }}</q-item-label>
        </q-card-section>
      </q-card>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';

const products = ref<
  Array<{
    id: number;
    name: string;
    price: number;
    image: string; // Added image field
  }>
>([]);

onMounted(async () => {
  try {
    const res = await fetch('/products.json'); // Ensure correct path for public assets
    if (!res.ok) {
      throw new Error(`HTTP error! status: ${res.status}`);
    }
    products.value = await res.json();
  } catch (error) {
    console.error('Failed to fetch products:', error);
    // Optionally, set products to an empty array or show an error message to the user
    products.value = [];
  }
});
</script>
