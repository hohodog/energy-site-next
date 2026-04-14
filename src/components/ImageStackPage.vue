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
  gap: clamp(16px, 1.8vw, 24px);
  width: min(100%, 1180px);
  margin: 0 auto;
  padding: clamp(12px, 2vw, 22px) clamp(12px, 2.6vw, 28px) 42px;
  background: transparent;
}

.image-frame {
  position: relative;
  margin: 0;
  padding: clamp(5px, 0.65vw, 8px);
  overflow: clip;
  border: 1px solid rgba(214, 222, 218, 0.96);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.96);
  box-shadow:
    0 1px 0 rgba(255, 255, 255, 0.78),
    0 12px 32px rgba(15, 31, 26, 0.07);
  content-visibility: auto;
  contain-intrinsic-size: auto 640px;
  transition:
    transform 0.2s ease,
    box-shadow 0.2s ease,
    border-color 0.2s ease;
}

.image-frame::before {
  content: '';
  position: absolute;
  inset: clamp(5px, 0.65vw, 8px);
  z-index: 1;
  border: 1px solid rgba(22, 49, 41, 0.07);
  border-radius: 5px;
  pointer-events: none;
}

.image-frame:hover {
  border-color: rgba(196, 208, 202, 0.96);
  box-shadow:
    0 1px 0 rgba(255, 255, 255, 0.82),
    0 16px 38px rgba(15, 31, 26, 0.1);
  transform: translateY(-1px);
}

.image-frame img {
  display: block;
  width: 100%;
  height: auto;
  border-radius: 6px;
  background: #ffffff;
}

@media (prefers-reduced-motion: reduce) {
  .image-frame {
    transition: none;
  }

  .image-frame:hover {
    transform: none;
  }
}

@media (max-width: 720px) {
  .image-stack-page {
    gap: 12px;
    padding-bottom: 30px;
  }

  .image-frame {
    box-shadow: 0 8px 20px rgba(15, 31, 26, 0.06);
    contain-intrinsic-size: auto 360px;
  }

  .image-frame:hover {
    transform: none;
  }
}
</style>
