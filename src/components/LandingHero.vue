<template>
  <main class="hero">
    <p class="eyebrow">Booking Made Smooth</p>
    <h1>Build better reservations from the very first click.</h1>
    <p class="hero-copy">
      A clean and modern foundation for your booking website, ready for your
      features, calendar flows, and customer journey.
    </p>
  </main>
</template>

<style scoped>
.hero {
  max-width: 760px;
  animation: revealUp 620ms ease both;
}

.eyebrow {
  margin: 0;
  color: var(--brand);
  text-transform: uppercase;
  letter-spacing: 0.14em;
  font-weight: 800;
  font-size: 0.77rem;
}

.hero h1 {
  margin: 14px 0 16px;
  font-family: "Space Grotesk", "Manrope", sans-serif;
  font-weight: 700;
  font-size: clamp(2rem, 5vw, 3.9rem);
  line-height: 1.03;
  letter-spacing: -0.02em;
  color: var(--heading);
}

.hero-copy {
  margin: 0;
  font-size: clamp(1rem, 2vw, 1.18rem);
  line-height: 1.62;
  max-width: 60ch;
}

@keyframes revealUp {
  from {
    opacity: 0;
    transform: translateY(16px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
