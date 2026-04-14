<script setup>
import { onMounted, onUnmounted, ref, watch } from 'vue'
import { useRoute } from 'vue-router'

defineOptions({ name: 'SiteNavbar' })

const menuItems = [
  { label: 'Home', path: '/' },
  { label: 'Sodium-ion batteries', path: '/sodium' },
  { label: 'Supercapacitors', path: '/supercapacitor' },
  { label: 'Flow Batteries', path: '/redox' },
  { label: 'solid-state batteries', path: '/solid' },
  { label: 'About', path: '/about' },
]

const route = useRoute()
const scrolled = ref(false)
const menuOpen = ref(false)

const syncScrollState = () => {
  scrolled.value = window.scrollY > 12
}

const closeMenu = () => {
  menuOpen.value = false
}

watch(
  () => route.fullPath,
  () => {
    closeMenu()
  },
)

onMounted(() => {
  syncScrollState()
  window.addEventListener('scroll', syncScrollState, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', syncScrollState)
})
</script>

<template>
  <header :class="['site-nav', { 'site-nav-scrolled': scrolled, 'site-nav-open': menuOpen }]">
    <div class="section-wrap">
      <div class="nav-shell">
        <RouterLink class="brand" to="/" @click="closeMenu">
          <span class="brand-mark" aria-hidden="true">SL</span>
          <span class="brand-copy">
            <strong>StorageLink</strong>
            <span>EU-facing Battery Sourcing</span>
          </span>
        </RouterLink>

        <nav class="nav-links" aria-label="Primary">
          <RouterLink
            v-for="item in menuItems"
            :key="item.path"
            :to="item.path"
            class="nav-link"
            exact-active-class="nav-link-active"
          >
            {{ item.label }}
          </RouterLink>
        </nav>

        <div class="nav-actions">
          <RouterLink class="nav-contact" to="/contact">Contact</RouterLink>

          <button
            class="menu-toggle"
            type="button"
            :aria-expanded="menuOpen ? 'true' : 'false'"
            aria-label="Toggle navigation"
            @click="menuOpen = !menuOpen"
          >
            <span></span>
            <span></span>
            <span></span>
          </button>
        </div>
      </div>

      <transition name="mobile-fade">
        <div v-if="menuOpen" class="mobile-panel">
          <nav class="mobile-links" aria-label="Mobile">
            <RouterLink
              v-for="item in menuItems"
              :key="`mobile-${item.path}`"
              :to="item.path"
              class="mobile-link"
              exact-active-class="mobile-link-active"
              @click="closeMenu"
            >
              {{ item.label }}
            </RouterLink>
            <RouterLink to="/contact" class="mobile-link mobile-link-cta" @click="closeMenu">
              Contact
            </RouterLink>
          </nav>
        </div>
      </transition>
    </div>
  </header>
</template>

<style scoped>
.site-nav {
  position: sticky;
  top: 0;
  z-index: 1200;
  padding: 20px 0 0;
  transition:
    padding 0.22s ease,
    transform 0.22s ease;
}

.site-nav::before {
  content: '';
  position: absolute;
  inset: 0 0 auto;
  height: 112px;
  background: linear-gradient(180deg, rgba(243, 246, 243, 0.94), rgba(243, 246, 243, 0));
  pointer-events: none;
}

.site-nav-scrolled,
.site-nav-open {
  padding-top: 12px;
}

.nav-shell,
.mobile-panel {
  border: 1px solid rgba(219, 225, 221, 0.92);
  border-radius: 24px;
  background: rgba(255, 255, 255, 0.86);
  box-shadow:
    0 18px 42px rgba(15, 31, 26, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.72);
  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);
}

.nav-shell {
  display: flex;
  align-items: center;
  gap: 20px;
  min-height: 78px;
  padding: 12px 14px 12px 20px;
}

.brand {
  display: inline-flex;
  align-items: center;
  gap: 14px;
  min-width: 0;
  margin-right: auto;
  color: inherit;
  text-decoration: none;
  flex-shrink: 0;
}

.brand-mark {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 42px;
  height: 42px;
  flex: 0 0 42px;
  border-radius: 14px;
  background:
    radial-gradient(circle at 30% 30%, rgba(255, 255, 255, 0.28), rgba(255, 255, 255, 0) 42%),
    linear-gradient(135deg, #163d34 0%, #1d8b98 100%);
  color: #f7fbf9;
  font-size: 13px;
  font-weight: 800;
  letter-spacing: 0.08em;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.24),
    0 10px 24px rgba(18, 52, 43, 0.16);
}

.brand-copy {
  display: grid;
  gap: 3px;
  min-width: 0;
}

.brand-copy strong {
  color: #17342c;
  font-size: 15px;
  font-weight: 800;
  letter-spacing: 0.01em;
  line-height: 1.1;
}

.brand-copy span {
  color: #72857d;
  font-size: 10px;
  letter-spacing: 0.16em;
  text-transform: uppercase;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 6px;
  border: 1px solid rgba(226, 231, 228, 0.9);
  border-radius: 999px;
  background: rgba(247, 249, 247, 0.9);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.92);
}

.nav-link,
.mobile-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 999px;
  color: #324840;
  text-decoration: none;
  font-size: 13px;
  font-weight: 700;
  padding: 11px 16px;
  transition:
    background 0.2s ease,
    color 0.2s ease,
    box-shadow 0.2s ease,
    transform 0.2s ease;
}

.nav-link:hover,
.mobile-link:hover,
.nav-link-active,
.mobile-link-active {
  color: #14362d;
  background: #ffffff;
  box-shadow: 0 6px 14px rgba(17, 45, 37, 0.08);
}

.brand:hover,
.brand:focus-visible,
.nav-link:hover,
.nav-link:focus-visible,
.nav-link-active,
.mobile-link:hover,
.mobile-link:focus-visible,
.mobile-link-active,
.nav-contact:hover,
.nav-contact:focus-visible {
  text-decoration: none;
}

.nav-actions {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-shrink: 0;
}

.nav-contact {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 46px;
  padding: 0 18px;
  border-radius: 999px;
  color: #f7fffc;
  text-decoration: none;
  font-size: 14px;
  font-weight: 700;
  letter-spacing: 0.01em;
  background: linear-gradient(135deg, #163d34 0%, #1d8b98 100%);
  box-shadow: 0 12px 24px rgba(18, 52, 43, 0.16);
  transition:
    transform 0.2s ease,
    box-shadow 0.2s ease,
    opacity 0.2s ease;
}

.nav-contact:hover {
  transform: translateY(-1px);
  box-shadow: 0 14px 26px rgba(18, 52, 43, 0.2);
}

.nav-link::after,
.mobile-link::after,
.nav-contact::after,
.brand::after {
  display: none;
}

.menu-toggle {
  position: relative;
  display: none;
  width: 46px;
  height: 46px;
  padding: 0;
  border: 1px solid rgba(214, 221, 217, 0.95);
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.82);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.9);
}

.menu-toggle span {
  position: absolute;
  left: 12px;
  right: 12px;
  height: 2px;
  border-radius: 999px;
  background: #183a31;
}

.menu-toggle span:nth-child(1) {
  top: 15px;
}

.menu-toggle span:nth-child(2) {
  top: 22px;
}

.menu-toggle span:nth-child(3) {
  top: 29px;
}

.mobile-panel {
  margin-top: 10px;
  padding: 12px;
  border-radius: 22px;
}

.mobile-links {
  display: grid;
  gap: 8px;
}

.mobile-link {
  justify-content: flex-start;
  padding: 13px 14px;
  border-radius: 14px;
  background: rgba(248, 250, 248, 0.8);
}

.mobile-link-cta {
  justify-content: center;
  margin-top: 6px;
  color: #f6fffc;
  background: linear-gradient(135deg, #163d34 0%, #1d8b98 100%);
}

.mobile-fade-enter-active,
.mobile-fade-leave-active {
  transition:
    opacity 0.2s ease,
    transform 0.2s ease;
}

.mobile-fade-enter-from,
.mobile-fade-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}

@media (max-width: 1180px) {
  .nav-links,
  .nav-contact {
    display: none;
  }

  .menu-toggle {
    display: block;
  }
}

@media (max-width: 720px) {
  .site-nav {
    padding-top: 14px;
  }

  .nav-shell {
    min-height: 70px;
    padding-left: 14px;
    padding-right: 12px;
  }

  .brand-copy span {
    display: none;
  }

  .brand-copy strong {
    font-size: 14px;
  }

  .brand-mark {
    width: 38px;
    height: 38px;
    flex-basis: 38px;
    border-radius: 12px;
    font-size: 12px;
  }
}
</style>
