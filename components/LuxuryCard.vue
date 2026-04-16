<template>
  <div class="card">
    <img :src="product.image" alt="">
    <h3>{{ product.title }}</h3>
    <p class="price">${{ product.price }}</p>

    <NuxtLink :to="`/producto/${product.id}`" class="btn">
      Ver detalles
    </NuxtLink>
  </div>
</template>

<script setup>
defineProps(['product'])
</script>
