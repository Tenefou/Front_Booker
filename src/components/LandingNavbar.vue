<template>
  <header class="navbar">
    <div class="brand-block">
      <div
        class="logo-placeholder"
        role="img"
        aria-label="Your logo placeholder"
      >
        LOGO
      </div>
      <p class="brand-title">Booker</p>
    </div>
    <div class="actions">
      <button
        class="secondary-button"
        type="button"
        @click="emit('open-client')"
      >
        Clients
      </button>
      <button class="cta-button" type="button" @click="emit('open-enterprise')">
        Entreprises
      </button>
    </div>
  </header>
</template>

<script setup lang="ts">
const emit = defineEmits<{
  (e: "open-enterprise"): void;
  (e: "open-client"): void;
}>();
</script>

<style scoped>
.navbar {
  display: flex;
  align-items: start;
  justify-content: space-between;
  gap: 18px;
}

.actions {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
  justify-content: flex-end;
}

.brand-block {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-placeholder {
  width: 52px;
  height: 52px;
  border-radius: 14px;
  border: 1px dashed rgba(14, 116, 144, 0.45);
  background: rgba(255, 255, 255, 0.9);
  color: var(--brand);
  font-size: 0.64rem;
  font-weight: 800;
  letter-spacing: 0.09em;
  display: grid;
  place-items: center;
}

.brand-title {
  margin: 0;
  font-family: "Space Grotesk", "Manrope", sans-serif;
  font-size: clamp(1.2rem, 1.6vw, 1.5rem);
  font-weight: 700;
  color: var(--heading);
}

.secondary-button,
.cta-button {
  border: none;
  border-radius: 999px;
  font-family: "Space Grotesk", "Manrope", sans-serif;
  font-weight: 700;
  font-size: 0.95rem;
  padding: 0.78rem 1.34rem;
  cursor: pointer;
  transition:
    transform 180ms ease,
    background-color 180ms ease,
    box-shadow 180ms ease,
    color 180ms ease,
    border-color 180ms ease;
}

.secondary-button {
  background: rgba(14, 116, 144, 0.08);
  color: var(--heading);
  border: 1px solid rgba(14, 116, 144, 0.12);
}

.cta-button {
  background: var(--accent);
  color: #fff;
}

.secondary-button:hover {
  background: rgba(14, 116, 144, 0.14);
}

.cta-button:hover {
  background: var(--accent-hover);
  transform: translateY(-1px);
  box-shadow: 0 14px 24px rgba(234, 88, 12, 0.28);
}

.secondary-button:focus-visible,
.cta-button:focus-visible {
  outline: 3px solid rgba(14, 116, 144, 0.25);
  outline-offset: 3px;
}

@media (max-width: 760px) {
  .navbar {
    gap: 10px;
  }

  .actions {
    width: 100%;
    justify-content: flex-start;
  }

  .logo-placeholder {
    width: 44px;
    height: 44px;
    border-radius: 12px;
  }

  .secondary-button,
  .cta-button {
    font-size: 0.86rem;
    padding: 0.68rem 1rem;
  }

  .actions .secondary-button,
  .actions .cta-button {
    flex: 1 1 140px;
  }
}
</style>
