<template>
  <q-page class="row items-center justify-evenly">
    <example-component
      title="Example component"
      active
      :todos="todos"
      :meta="meta"
    ></example-component>

    <q-card class="col-4">
      <q-card-section>
        <q-card-title>Products</q-card-title>
      </q-card-section>

      <q-card-section>
        <q-list bordered>
          <q-item v-for="product in products" :key="product.id" clickable v-ripple>
            <q-item-section>
              <q-item-label>{{ product.name }}</q-item-label>
              <q-item-label caption>Price: {{ product.price }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup lang="ts">
import ExampleComponent from 'components/ExampleComponent.vue';
import type { Meta, Todo } from 'components/models';
import { onMounted, ref } from 'vue';

const todos = ref<Todo[]>([
  {
    id: 1,
    content: 'ct1',
  },
  {
    id: 2,
    content: 'ct2',
  },
  {
    id: 3,
    content: 'ct3',
  },
  {
    id: 4,
    content: 'ct4',
  },
  {
    id: 5,
    content: 'ct5',
  },
]);

const meta = ref<Meta>({
  totalCount: 1200,
});

const products = ref<
  Array<{
    id: number;
    name: string;
    price: number;
  }>
>([]);

onMounted(async () => {
  await fetch('./products.json').then(async (res) => {
    products.value = await res.json();
  });
});
</script>
