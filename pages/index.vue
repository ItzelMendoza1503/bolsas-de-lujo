<script setup>
// Datos locales para evitar fallos de conexión a la API a última hora
const bolsas = [
  { id: 1, nombre: "Mochila Classic Canvas", precio: 120, img: "https://images.unsplash.com/photo-1553062407-98eeb64c6a62?w=500&q=80" },
  { id: 2, nombre: "Bolso de Cuero Elegance", precio: 350, img: "https://images.unsplash.com/photo-1584917865442-de89df76afd3?w=500&q=80" },
  { id: 3, nombre: "Maletín Ejecutivo Pro", precio: 280, img: "https://images.unsplash.com/photo-1548036328-c9fa89d128fa?w=500&q=80" },
  { id: 4, nombre: "Morral Urbano Minimal", precio: 95, img: "https://images.unsplash.com/photo-1622560480605-d83c853bc5c3?w=500&q=80" }
]
</script>

<template>
  <div style="font-family: 'Segoe UI', sans-serif; padding: 20px; background: #fdfdfd; min-height: 100vh;">
    <header style="text-align: center; border-bottom: 2px solid #1a1a1a; margin-bottom: 40px; background: white; padding: 30px;">
      <h1 style="margin: 0; letter-spacing: 3px; text-transform: uppercase;">Catálogo de Bolsos</h1>
      <p style="color: #666; margin-top: 10px;">Proyecto Final - Desarrollo Web SSR</p>
    </header>

    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 30px; max-width: 1200px; margin: 0 auto;">
      <div v-for="b in bolsas" :key="b.id" style="background: white; border: 1px solid #eee; padding: 20px; text-align: center; border-radius: 15px; box-shadow: 0 10px 20px rgba(0,0,0,0.05); transition: 0.3s;">
        <img :src="b.img" style="width: 100%; height: 220px; object-fit: cover; border-radius: 10px; margin-bottom: 15px;">
        <h3 style="color: #333;">{{ b.nombre }}</h3>
        <p style="font-weight: bold; color: #b08d57; font-size: 1.3rem; margin: 10px 0;">${{ b.precio }} USD</p>
        <button style="background: #1a1a1a; color: white; border: none; padding: 12px 20px; cursor: pointer; border-radius: 5px; width: 100%; font-weight: bold; letter-spacing: 1px;">
          VER DETALLES
        </button>
      </div>
    </div>
  </div>
</template>