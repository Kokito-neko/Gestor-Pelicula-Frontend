<script setup lang="ts">
import { onMounted } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

onMounted(() => {
  const token = localStorage.getItem("token");
  if (!token) {
    router.push("/login");
  }
});

const cerrarSesion = () => {
  localStorage.removeItem("token");
  router.push("/login");
};
</script>

<template>
  <div class="movies-container">
    <header class="movies-header">
      <h1>🎬 Catálogo de Películas</h1>
      <button @click="cerrarSesion" class="btn-logout">Cerrar Sesión</button>
    </header>

    <main class="movies-content">
      <div class="welcome-banner">
        <h2>¡Bienvenido a tu plataforma!</h2>
        <p>Has iniciado sesión correctamente y tu token está activo.</p>
      </div>
    </main>
  </div>
</template>

<style lang="css" scoped>
.movies-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2.5rem 1.5rem;
}

.movies-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
  border-bottom: 1px solid var(--color7);
  padding-bottom: 1rem;
}

h1 {
  font-size: 2rem;
  font-weight: 700;
  color: var(--color4);
}

.btn-logout {
  background-color: #e50914;
  color: white;
  border: none;
  padding: 0.6rem 1.2rem;
  border-radius: 6px;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.btn-logout:hover {
  background-color: #b20710;
}

.welcome-banner {
  background-color: var(--color3);
  border: 1px solid var(--color7);
  border-radius: 12px;
  padding: 2rem;
  text-align: center;
}

.welcome-banner h2 {
  color: var(--color4);
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.welcome-banner p {
  color: var(--color8);
  font-size: 1rem;
}
</style>