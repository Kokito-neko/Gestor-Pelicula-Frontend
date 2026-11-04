<script setup lang="ts">
import { ref } from 'vue';

const title = ref("Gestor de Películas");
const subtitle = ref("Bienvenido a tu catálogo personalizado de cine");
</script>

<template>
  <div class="home-container">
    <div class="hero-card">
      <h1>{{ title }}</h1>
      <p>{{ subtitle }}</p>
      <div class="actions">
        <router-link to="/login" class="btn-primary">Iniciar Sesión</router-link>
      </div>
    </div>
  </div>
</template>

<style lang="css" scoped>
.home-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 60vh;
  padding: 2rem;
}

.hero-card {
  background-color: var(--color3);
  border: 1px solid var(--color7);
  border-radius: 12px;
  padding: 3rem 2rem;
  text-align: center;
  max-width: 600px;
  width: 100%;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
}

h1 {
  font-size: 2.2rem;
  font-weight: 700;
  color: var(--color4);
  margin-bottom: 0.8rem;
}

p {
  color: var(--color8);
  font-size: 1.1rem;
  margin-bottom: 2rem;
}

.btn-primary {
  display: inline-block;
  background-color: var(--color4);
  color: var(--color2);
  padding: 0.8rem 1.8rem;
  border-radius: 6px;
  text-decoration: none;
  font-weight: 600;
  transition: background-color 0.2s ease;
}

.btn-primary:hover {
  background-color: var(--color5);
}
</style>