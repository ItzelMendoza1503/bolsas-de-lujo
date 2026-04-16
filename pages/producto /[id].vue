<template>
  <div v-if="product" style="padding:20px;">
    <h1>{{ product.title }}</h1>

    <img :src="product.image" width="250" />

    <p>{{ product.description }}</p>

    <h2>${{ product.price }}</h2>

    <NuxtLink to="/" class="btn">Volver</NuxtLink>
  </div>
</template>

<script setup>
const route = useRoute()

const { data: product } = await useFetch(
  `https://fakestoreapi.com/products/${route.params.id}`
)
</script>