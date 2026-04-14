<script setup>
defineProps({
  images: {
    type: Array,
    required: true,
  },
})
</script>

<template>
  <section class="image-stack-page" aria-label="Page image content">
    <figure v-for="(image, index) in images" :key="image.src" class="image-frame">
      <img
        :src="image.src"
        :srcset="image.srcset"
        :sizes="image.sizes"
        :alt="image.alt"
        :width="image.width"
        :height="image.height"
        :loading="index === 0 ? 'eager' : 'lazy'"
        :fetchpriority="index === 0 ? 'high' : undefined"
        decoding="async"
      />
    </figure>
  </section>
</template>

<style scoped>
.image-stack-page {
  display: grid;
  gap: clamp(14px, 2vw, 22px);
  width: min(100%, 1440px);
  margin: 0 auto;
  padding: clamp(14px, 2vw, 24px) clamp(14px, 2vw, 28px) 44px;
  background: transparent;
}

.image-frame {
  position: relative;
  margin: 0;
  padding: clamp(6px, 0.8vw, 10px);
  border: 1px solid rgba(219, 225, 221, 0.92);
  border-radius: 0;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.92), rgba(249, 251, 250, 0.86));
  box-shadow:
    0 1px 0 rgba(255, 255, 255, 0.76),
    0 18px 42px rgba(15, 31, 26, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.78),
    inset 0 0 0 1px rgba(255, 255, 255, 0.52);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  transition:
    transform 0.2s ease,
    box-shadow 0.2s ease,
    border-color 0.2s ease;
}

.image-frame::before {
  content: '';
  position: absolute;
  inset: clamp(6px, 0.8vw, 10px);
  z-index: 1;
  border: 1px solid rgba(22, 49, 41, 0.08);
  pointer-events: none;
}

.image-frame:hover {
  border-color: rgba(196, 208, 202, 0.96);
  box-shadow:
    0 1px 0 rgba(255, 255, 255, 0.82),
    0 24px 54px rgba(15, 31, 26, 0.12),
    0 8px 20px rgba(15, 31, 26, 0.06),
    inset 0 1px 0 rgba(255, 255, 255, 0.82),
    inset 0 0 0 1px rgba(255, 255, 255, 0.6);
  transform: translateY(-2px);
}

.image-frame img {
  display: block;
  width: 100%;
  height: auto;
  border-radius: 0;
}

@media (prefers-reduced-motion: reduce) {
  .image-frame {
    transition: none;
  }

  .image-frame:hover {
    transform: none;
  }
}
</style>
