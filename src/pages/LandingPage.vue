<script setup lang="ts">
import { ref } from "vue";

import LandingHero from "../components/LandingHero.vue";
import LandingNavbar from "../components/LandingNavbar.vue";
import SignupModal from "../components/SignupModal.vue";

const isSignupModalOpen = ref(false);
const modalContextLabel = ref("Compte client");

function openSignupModal(contextLabel = "Compte client") {
  modalContextLabel.value = contextLabel;
  isSignupModalOpen.value = true;
}

function closeSignupModal() {
  isSignupModalOpen.value = false;
}
</script>

<template>
  <div class="page-shell">
    <LandingNavbar
      @open-enterprise="openSignupModal('Compte entreprise')"
      @open-client="openSignupModal('Compte client')"
    />
    <LandingHero />
  </div>

  <SignupModal
    :open="isSignupModalOpen"
    :context-label="modalContextLabel"
    @close="closeSignupModal"
  />
</template>

<style scoped>
.page-shell {
  min-height: calc(100svh - 52px);
  border: 1px solid var(--line);
  border-radius: 28px;
  background: var(--paper);
  backdrop-filter: blur(5px);
  box-shadow: var(--shadow);
  padding: 26px clamp(20px, 4vw, 52px) clamp(40px, 6vw, 76px);
  display: grid;
  gap: clamp(40px, 8vw, 84px);
}

@media (max-width: 760px) {
  .page-shell {
    min-height: calc(100svh - 28px);
    border-radius: 20px;
    padding: 18px 16px 36px;
    gap: 32px;
  }
}
</style>
