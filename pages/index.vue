<script setup>
// Usamos la API de DummyJSON para simular productos de lujo (bolsos)
const { data: productos } = await useFetch('https://dummyjson.com/products/category/womens-bags')
</script>

<template>
  <div style="background-color: #fcfaf8; min-height: 100vh; font-family: 'Helvetica Neue', Arial, sans-serif; padding-bottom: 50px;">
    
    <header style="text-align: center; padding: 60px 20px; background-color: white; border-bottom: 1px solid #eee;">
      <h1 style="letter-spacing: 8px; text-transform: uppercase; font-weight: 300; color: #1a1a1a; margin: 0;">Catálogo de Bolsos</h1>
      <p style="color: #b08d57; font-size: 0.9rem; margin-top: 10px; letter-spacing: 2px;">Proyecto Final - Desarrollo Web SSR</p>
    </header>

    <main style="max-width: 1200px; margin: 0 auto; padding: 40px 20px;">
      <div v-if="productos" style="display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 30px;">
        
        <div v-for="item in productos.products" :key="item.id" 
          style="background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 4px 15px rgba(0,0,0,0.05); transition: transform 0.3s ease;">
          
          <img :src="item.thumbnail" :alt="item.title" style="width: 100%; height: 250px; object-fit: cover;">
          
          <div style="padding: 20px; text-align: center;">
            <h3 style="font-size: 1.1rem; color: #333; margin-bottom: 8px; height: 50px; overflow: hidden;">{{ item.title }}</h3>
            <p style="color: #b08d57; font-weight: bold; font-size: 1.2rem;">${{ item.price }} USD</p>
            
            <button style="margin-top: 15px; background: #1a1a1a; color: white; border: none; padding: 10px 25px; cursor: pointer; border-radius: 4px; font-size: 0.8rem; letter-spacing: 1px;">
              VER DETALLES
            </button>
          </div>
        </div>
      </div>

      <div v-else style="text-align: center; padding: 50px;">
        <p>Cargando colección exclusiva...</p>
      </div>

      <section style="margin-top: 80px; text-align: center; padding: 60px; background-color: white; border-radius: 15px; border: 1px solid #f0e6d2;">
        <h2 style="color: #1a1a1a; text-transform: uppercase; letter-spacing: 3px; font-size: 1.5rem;">¿Buscas un diseño personalizado?</h2>
        <p style="color: #666; margin-bottom: 30px;">Si no encuentras el modelo ideal en nuestro catálogo, contáctanos para una asesoría VIP.</p>
        
        <NuxtLink to="/contacto" 
          style="display: inline-block; background: #1a1a1a; color: #d4af37; padding: 18px 40px; text-decoration: none; font-weight: bold; border-radius: 5px; border: 2px solid #1a1a1a; transition: 0.3s; letter-spacing: 2px;">
          IR AL FORMULARIO DE CONTACTO
        </NuxtLink>
      </section>

    </main>

    <footer style="text-align: center; color: #999; font-size: 0.8rem; padding: 40px 0;">
      &copy; 2026 Boutique de Lujo - Itzel Mendoza
    </footer>
  </div>
</template>

<style scoped>
/* Efecto al pasar el mouse sobre las tarjetas */
div[style*="transition"] :hover {
  transform: translateY(-5px);
}
</style>