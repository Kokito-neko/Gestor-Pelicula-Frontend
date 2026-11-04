<script lang="ts" setup>
import { toTypedSchema } from "@vee-validate/zod";
import * as z from "zod";
import { useForm } from "vee-validate";
import { useRouter } from "vue-router";

const router = useRouter();
const BACKEND_URL = import.meta.env.VITE_BACKEND_URL || "http://localhost:3000";

const schema = toTypedSchema(
  z.object({
    email: z
      .string({ message: "El correo es obligatorio" })
      .email({ message: "El correo es inválido." }),
    password: z
      .string({ message: "La contraseña es obligatoria" })
      .min(8, { message: "La contraseña debe tener mínimo 8 caracteres" }), // 👈 Actualizado a 8 caracteres para sincronizar con .NET
  })
);

const { errors, handleSubmit, defineField } = useForm({
  validationSchema: schema,
});

const [email, emailAttrs] = defineField("email");
const [password, passwordAttrs] = defineField("password");

const onSubmit = handleSubmit(async (values) => {
  try {
    const request = await fetch(`${BACKEND_URL}/api/v1/auth/login`, {
      headers: {
        "Content-Type": "application/json;charset=utf-8",
      },
      body: JSON.stringify(values),
      method: "POST",
    });

    const response = await request.json();
    console.log("ESTO DEVUELVE EL BACKEND:", response);

    if (request.ok && response.token) {
      localStorage.setItem("token", response.token);
      router.push("/movies");
    } else {
      alert(response.message || "Error al iniciar sesión");
    }
  } catch (error) {
    console.error("Error al conectar:", error);
    alert("Ocurrió un error al intentar conectar con el servidor.");
  }
});
</script>

<template>
  <div class="login-wrapper">
    <div class="login-card">
      <div class="brand-header">
        <h1 class="title">🎬 Gestor de Películas</h1>
        <p class="subtitle">Ingresa tus credenciales para acceder a la plataforma</p>
      </div>

      <form class="form" @submit.prevent="onSubmit">
        <fieldset class="form__fieldset">
          <label class="form__label">Correo Electrónico</label>
          <input
            class="form__input"
            type="email"
            placeholder="usuario@ejemplo.com"
            v-model="email"
            v-bind="emailAttrs"
            :class="{ 'form__input--error': errors.email }"
          />
          <span v-if="errors.email" class="error-msg">{{ errors.email }}</span>
        </fieldset>

        <fieldset class="form__fieldset">
          <label class="form__label">Contraseña</label>
          <input
            class="form__input"
            type="password"
            placeholder="••••••••"
            v-model="password"
            v-bind="passwordAttrs"
            :class="{ 'form__input--error': errors.password }"
          />
          <span v-if="errors.password" class="error-msg">{{ errors.password }}</span>
        </fieldset>

        <button class="form__btn" type="submit">Iniciar Sesión</button>
      </form>
    </div>
  </div>
</template>

<style lang="css" scoped>
.login-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 75vh;
  padding: 1.5rem;
}

.login-card {
  background-color: var(--color3);
  border: 1px solid var(--color7);
  border-radius: 12px;
  padding: 2.5rem 2rem;
  width: 100%;
  max-width: 420px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.6);
}

.brand-header {
  text-align: center;
  margin-bottom: 2rem;
}

.title {
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--color4);
  margin-bottom: 0.4rem;
}

.subtitle {
  color: var(--color8);
  font-size: 0.9rem;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.form__fieldset {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  border: none;
  padding: 0;
  margin: 0;
}

.form__label {
  font-size: 0.85rem;
  font-weight: 500;
  color: var(--color2);
}

.form__input {
  width: 100%;
  padding: 0.75rem 1rem;
  background-color: var(--color1);
  border: 1px solid var(--color7);
  border-radius: 6px;
  color: var(--color2);
  font-size: 0.95rem;
  outline: none;
  transition: border-color 0.2s ease;
}

.form__input:focus {
  border-color: var(--color4);
}

.form__input--error {
  border-color: var(--errorColor) !important;
}

.error-msg {
  color: var(--errorColor);
  font-size: 0.8rem;
  margin-top: 0.2rem;
}

.form__btn {
  margin-top: 0.5rem;
  padding: 0.85rem;
  background-color: var(--color4);
  color: var(--color2);
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.form__btn:hover {
  background-color: var(--color5);
}
</style>-