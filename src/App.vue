<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header class="navbar">
    <div class="navbar-container">
      <div class="navbar-brand">
        <RouterLink to="/" class="brand-logo">CineApp</RouterLink>
      </div>
      <nav class="navbar-links">
        <RouterLink to="/" class="nav-link">Inicio</RouterLink>
        <RouterLink to="/login" class="nav-btn">Iniciar Sesión</RouterLink>
      </nav>
    </div>
  </header>

  <main class="main">
    <RouterView />
  </main>
</template>

<style lang="css" scoped>
.navbar {
  background-color: var(--color3);
  border-bottom: 1px solid var(--color7);
  padding: 1rem 2rem;
  position: sticky;
  top: 0;
  z-index: 100;
}

.navbar-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 75rem;
  margin: 0 auto;
}

.brand-logo {
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--color4);
  text-decoration: none;
  letter-spacing: 0.5px;
}

.navbar-links {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.nav-link {
  color: var(--color2);
  text-decoration: none;
  font-weight: 500;
  font-size: 0.95rem;
  transition: color 0.2s ease;
}

.nav-link:hover {
  color: var(--color4);
}

.nav-btn {
  background-color: var(--color4);
  color: var(--color2);
  padding: 0.5rem 1.2rem;
  border-radius: 6px;
  text-decoration: none;
  font-weight: 600;
  font-size: 0.9rem;
  transition: background-color 0.2s ease;
}

.nav-btn:hover {
  background-color: var(--color5);
}
</style>