<script setup>
const solutions = [
  { label: 'Sodium-ion batteries', path: '/sodium' },
  { label: 'Supercapacitors', path: '/supercapacitor' },
  { label: 'Flow Batteries', path: '/redox' },
  { label: 'solid-state batteries', path: '/solid' },
]

const companyLinks = [
  { label: 'About', path: '/about' },
  { label: 'Contact', path: '/contact' },
]

const focusAreas = [
  'Battery technology screening',
  'Supplier connection in China',
  'Cross-border technical coordination',
]
</script>

<template>
  <footer class="site-footer">
    <div class="section-wrap">
      <div class="footer-shell">
        <section class="footer-top">
          <div class="footer-brand-block">
            <RouterLink class="footer-brand" to="/">
              <span class="footer-brand-mark" aria-hidden="true">SL</span>
              <span class="footer-brand-copy">
                <strong>StorageLink</strong>
                <span>EU-facing Battery Sourcing</span>
              </span>
            </RouterLink>

            <p class="footer-intro">
              We help European projects connect with suitable battery technologies and qualified
              manufacturing resources in China, with a focus on practical execution rather than
              generic sourcing advice.
            </p>
          </div>

          <div class="footer-grid">
            <nav class="footer-column" aria-label="Solutions">
              <p class="footer-heading">Solutions</p>
              <RouterLink
                v-for="item in solutions"
                :key="item.path"
                :to="item.path"
                class="footer-link"
              >
                {{ item.label }}
              </RouterLink>
            </nav>

            <nav class="footer-column" aria-label="Company">
              <p class="footer-heading">Company</p>
              <RouterLink
                v-for="item in companyLinks"
                :key="item.path"
                :to="item.path"
                class="footer-link"
              >
                {{ item.label }}
              </RouterLink>
            </nav>

            <section class="footer-column" aria-label="Focus areas">
              <p class="footer-heading">Focus</p>
              <ul class="footer-list">
                <li v-for="item in focusAreas" :key="item">{{ item }}</li>
              </ul>
            </section>
          </div>
        </section>

        <section class="footer-bottom">
          <p class="footer-meta">
            © 2026 StorageLink. Built for structured cross-border energy collaboration.
          </p>
          <div class="footer-bottom-links">
            <RouterLink to="/about" class="footer-mini-link">How we work</RouterLink>
            <RouterLink to="/contact" class="footer-mini-link footer-mini-link-accent">
              Contact
            </RouterLink>
          </div>
        </section>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.site-footer {
  padding: 28px 0 44px;
}

.footer-shell {
  border: 1px solid rgba(218, 224, 220, 0.92);
  border-radius: 28px;
  background:
    linear-gradient(180deg, rgba(251, 252, 251, 0.96), rgba(246, 248, 246, 0.96)),
    linear-gradient(135deg, rgba(28, 141, 157, 0.03), rgba(22, 61, 52, 0.04));
  box-shadow:
    0 18px 44px rgba(15, 31, 26, 0.06),
    inset 0 1px 0 rgba(255, 255, 255, 0.75);
  overflow: hidden;
}

.footer-top {
  display: grid;
  grid-template-columns: minmax(0, 1.15fr) minmax(0, 1fr);
  gap: 48px;
  padding: 36px 40px 30px;
}

.footer-brand-block {
  max-width: 520px;
}

.footer-brand {
  display: inline-flex;
  align-items: center;
  gap: 14px;
  color: inherit;
  text-decoration: none;
}

.footer-brand-mark {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  flex: 0 0 44px;
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
    0 10px 24px rgba(18, 52, 43, 0.14);
}

.footer-brand-copy {
  display: grid;
  gap: 3px;
}

.footer-brand-copy strong {
  color: #17342c;
  font-size: 16px;
  font-weight: 800;
  letter-spacing: 0.01em;
  line-height: 1.1;
}

.footer-brand-copy span {
  color: #72857d;
  font-size: 10px;
  letter-spacing: 0.16em;
  text-transform: uppercase;
}

.footer-intro {
  margin: 22px 0 0;
  color: #546760;
  font-size: 14px;
  line-height: 1.8;
}

.footer-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 28px;
}

.footer-column {
  min-width: 0;
}

.footer-heading {
  margin: 0 0 14px;
  color: #17342c;
  font-size: 12px;
  font-weight: 800;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

.footer-link,
.footer-mini-link {
  color: #4d6159;
  text-decoration: none;
  transition:
    color 0.2s ease,
    opacity 0.2s ease;
}

.footer-link {
  display: block;
  padding: 9px 0;
  font-size: 14px;
  line-height: 1.5;
}

.footer-link:hover,
.footer-link:focus-visible,
.footer-mini-link:hover,
.footer-mini-link:focus-visible,
.footer-brand:hover,
.footer-brand:focus-visible {
  color: #14362d;
  text-decoration: none;
}

.footer-list {
  margin: 0;
  padding: 0;
  list-style: none;
}

.footer-list li {
  position: relative;
  padding: 9px 0 9px 16px;
  color: #4d6159;
  font-size: 14px;
  line-height: 1.6;
}

.footer-list li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 18px;
  width: 6px;
  height: 6px;
  border-radius: 999px;
  background: rgba(29, 139, 152, 0.5);
}

.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 18px;
  padding: 18px 40px 22px;
  border-top: 1px solid rgba(223, 228, 225, 0.92);
}

.footer-meta {
  margin: 0;
  color: #70827a;
  font-size: 13px;
  line-height: 1.6;
}

.footer-bottom-links {
  display: flex;
  align-items: center;
  gap: 18px;
  flex-wrap: wrap;
}

.footer-mini-link {
  font-size: 13px;
  font-weight: 700;
}

.footer-mini-link-accent {
  color: #173f35;
}

.footer-link::after,
.footer-mini-link::after,
.footer-brand::after {
  display: none;
}

@media (max-width: 1080px) {
  .footer-top {
    grid-template-columns: 1fr;
    gap: 34px;
  }

  .footer-brand-block {
    max-width: none;
  }
}

@media (max-width: 820px) {
  .site-footer {
    padding: 20px 0 34px;
  }

  .footer-top {
    padding: 28px 22px 24px;
  }

  .footer-grid {
    grid-template-columns: 1fr 1fr;
  }

  .footer-bottom {
    flex-direction: column;
    align-items: flex-start;
    padding: 18px 22px 22px;
  }
}

@media (max-width: 560px) {
  .footer-shell {
    border-radius: 22px;
  }

  .footer-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .footer-intro {
    font-size: 13px;
    line-height: 1.75;
  }

  .footer-brand-mark {
    width: 40px;
    height: 40px;
    flex-basis: 40px;
    border-radius: 13px;
  }

  .footer-brand-copy strong {
    font-size: 15px;
  }
}
</style>
