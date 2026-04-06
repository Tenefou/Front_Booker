<script setup lang="ts">
import { computed, ref, watch } from "vue";

const props = defineProps<{
  open: boolean;
  contextLabel?: string;
}>();

const emit = defineEmits<{
  (e: "close"): void;
}>();

const email = ref("");
const password = ref("");
const confirmPassword = ref("");
const errorMessage = ref("");
const isSubmitted = ref(false);

const dialogTitle = computed(() => {
  if (props.contextLabel?.toLowerCase().includes("entreprise")) {
    return "Créer un compte entreprise";
  }

  return "Créer un compte client";
});
const contextText = computed(() => props.contextLabel ?? "Compte client");

watch(
  () => props.open,
  (isOpen) => {
    if (!isOpen) {
      email.value = "";
      password.value = "";
      confirmPassword.value = "";
      errorMessage.value = "";
      isSubmitted.value = false;
    }
  },
);

function closeModal() {
  emit("close");
}

function handleSubmit() {
  errorMessage.value = "";

  if (
    !email.value.trim() ||
    !password.value.trim() ||
    !confirmPassword.value.trim()
  ) {
    errorMessage.value = "Merci de remplir tous les champs.";
    return;
  }

  if (password.value !== confirmPassword.value) {
    errorMessage.value = "Les mots de passe ne correspondent pas.";
    return;
  }

  isSubmitted.value = true;
}
</script>

<template>
  <Teleport to="body">
    <Transition name="modal-fade">
      <div v-if="open" class="modal-overlay" @click.self="closeModal">
        <section
          class="modal-card"
          role="dialog"
          aria-modal="true"
          aria-labelledby="signup-title"
        >
          <div class="modal-header">
            <div>
              <p class="modal-kicker">{{ contextText }}</p>
              <h2 id="signup-title">{{ dialogTitle }}</h2>
            </div>
            <button
              class="icon-button"
              type="button"
              aria-label="Fermer la fenêtre"
              @click="closeModal"
            >
              ×
            </button>
          </div>

          <p class="modal-copy">
            Crée ton accès avec une adresse email et un mot de passe confirmé.
          </p>

          <form
            v-if="!isSubmitted"
            class="signup-form"
            @submit.prevent="handleSubmit"
          >
            <label class="field-group">
              <span>Email</span>
              <input
                v-model="email"
                type="email"
                autocomplete="email"
                placeholder="vous@exemple.com"
              />
            </label>

            <label class="field-group">
              <span>Mot de passe</span>
              <input
                v-model="password"
                type="password"
                autocomplete="new-password"
                placeholder="Votre mot de passe"
              />
            </label>

            <label class="field-group">
              <span>Confirmer le mot de passe</span>
              <input
                v-model="confirmPassword"
                type="password"
                autocomplete="new-password"
                placeholder="Répétez votre mot de passe"
              />
            </label>

            <p v-if="errorMessage" class="error-message" role="alert">
              {{ errorMessage }}
            </p>

            <div class="modal-actions">
              <button class="ghost-button" type="button" @click="closeModal">
                Annuler
              </button>
              <button class="submit-button" type="submit">
                Créer mon compte
              </button>
            </div>
          </form>

          <div v-else class="success-state">
            <p class="success-title">Compte prêt à être créé.</p>
            <p class="success-copy">
              Tu peux maintenant connecter ce formulaire à ton backend ou à ton
              système d'authentification.
            </p>
            <button class="submit-button" type="button" @click="closeModal">
              Fermer
            </button>
          </div>
        </section>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  z-index: 50;
  display: grid;
  place-items: center;
  padding: 20px;
  background: rgba(12, 28, 47, 0.5);
  backdrop-filter: blur(10px);
}

.modal-card {
  width: min(100%, 540px);
  border-radius: 24px;
  border: 1px solid rgba(14, 116, 144, 0.18);
  background: rgba(255, 255, 255, 0.96);
  box-shadow: 0 30px 80px rgba(12, 28, 47, 0.22);
  padding: 24px;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  gap: 16px;
  align-items: start;
}

.modal-kicker {
  margin: 0 0 6px;
  color: var(--brand);
  text-transform: uppercase;
  letter-spacing: 0.14em;
  font-weight: 800;
  font-size: 0.75rem;
}

.modal-card h2 {
  margin: 0;
  font-family: "Space Grotesk", "Manrope", sans-serif;
  font-size: clamp(1.5rem, 3vw, 2rem);
  line-height: 1.05;
  color: var(--heading);
}

.icon-button {
  border: none;
  background: rgba(14, 116, 144, 0.08);
  color: var(--heading);
  width: 42px;
  height: 42px;
  border-radius: 12px;
  font-size: 1.5rem;
  line-height: 1;
  cursor: pointer;
}

.modal-copy {
  margin: 12px 0 22px;
  line-height: 1.6;
}

.signup-form {
  display: grid;
  gap: 16px;
}

.field-group {
  display: grid;
  gap: 8px;
  font-weight: 700;
  color: var(--heading);
}

.field-group span {
  font-size: 0.95rem;
}

.field-group input {
  width: 100%;
  border: 1px solid rgba(14, 116, 144, 0.22);
  border-radius: 16px;
  padding: 0.95rem 1rem;
  background: rgba(255, 255, 255, 0.96);
  color: var(--heading);
  font: inherit;
}

.field-group input:focus {
  outline: 3px solid rgba(234, 88, 12, 0.18);
  border-color: rgba(234, 88, 12, 0.45);
}

.error-message {
  margin: 0;
  color: #b91c1c;
  font-weight: 700;
}

.modal-actions {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
  margin-top: 6px;
}

.ghost-button,
.submit-button {
  border: none;
  border-radius: 999px;
  font-family: "Space Grotesk", "Manrope", sans-serif;
  font-weight: 700;
  padding: 0.82rem 1.2rem;
  cursor: pointer;
}

.ghost-button {
  background: rgba(14, 116, 144, 0.08);
  color: var(--heading);
}

.submit-button {
  background: var(--accent);
  color: #fff;
}

.success-state {
  display: grid;
  gap: 14px;
}

.success-title {
  margin: 0;
  font-family: "Space Grotesk", "Manrope", sans-serif;
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--heading);
}

.success-copy {
  margin: 0;
  line-height: 1.6;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition:
    opacity 180ms ease,
    transform 180ms ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
  transform: scale(0.98);
}

@media (max-width: 760px) {
  .modal-card {
    padding: 20px;
    border-radius: 20px;
  }

  .modal-actions {
    flex-direction: column-reverse;
  }

  .ghost-button,
  .submit-button {
    width: 100%;
  }
}
</style>
