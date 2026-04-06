<template>
  <div class="page-wrapper">

    <!-- ══════════════════════ NAVBAR ══════════════════════ -->
    <nav class="navbar">
      <a href="#" class="nav-logo">Proyecto academia</a>

      <div class="nav-links">
        <a
          v-for="link in navLinks"
          :key="link.label"
          :href="link.href"
          :class="['nav-link', { 'nav-link--active': link.active }]"
        >{{ link.label }}</a>
      </div>

      <a href="#" class="nav-cta">
        Inscribirme
        <ArrowRight :size="14" />
      </a>

      <!-- Mobile hamburger -->
      <button class="hamburger" @click="mobileMenuOpen = !mobileMenuOpen" aria-label="Menú">
        <Menu v-if="!mobileMenuOpen" :size="22" />
        <X v-else :size="22" />
      </button>
    </nav>

    <!-- Mobile menu -->
    <Transition name="slide-down">
      <div v-if="mobileMenuOpen" class="mobile-menu">
        <a v-for="link in navLinks" :key="link.label" href="#" class="mobile-link" @click="mobileMenuOpen = false">
          {{ link.label }}
        </a>
        <a href="#" class="nav-cta" style="margin: 16px;">Inscribirme <ArrowRight :size="14" /></a>
      </div>
    </Transition>

    <!-- ══════════════════════ HERO ══════════════════════ -->
    <section class="hero">
      <video class="hero-video" :src="videoUrl" autoplay loop muted playsinline />
      <!-- fade top & bottom into navbar / info-strip -->
      <div class="hero-fade-top" />
      <div class="hero-fade-bottom" />

      <!-- Content: upper-center positioning (matches reference ~25% from top) -->
      <div class="hero-content">
        <h1 class="hero-heading">
          <span class="hero-heading__line1">Tu futuro</span>
          <ShinyText base-color="#64CEFB" shine-color="#ffffff" :speed="3" :spread="100" class="hero-heading__line2">
            Comienza aquí.
          </ShinyText>
        </h1>

        <div class="hero-badge">
          <span class="hero-badge__dot" />
          Próximamente agregaremos nuevos cursos
        </div>

        <a href="#" class="hero-cta">
          Informarme sobre inscripciones
          <ArrowRight :size="16" class="hero-cta__icon" />
        </a>
      </div>
    </section>

    <!-- ══════════════════════ INFO STRIP ══════════════════════ -->
    <section class="info-strip">
      <div class="info-col info-col--empty" />
      <div class="info-col">
        <p class="info-text">
          Ofrecemos programas transformadores que empoderan a los diseñadores de
          producto emergentes con conocimientos de vanguardia y visión para
          triunfar a nivel global.
        </p>
      </div>
      <div class="info-col">
        <p class="info-text">
          Únete a una comunidad de diseñadores visionarios que están definiendo
          el futuro de los productos digitales a través del aprendizaje
          estructurado y la práctica real.
        </p>
      </div>
      <div class="info-col info-col--empty" />
    </section>

    <!-- ══════════════════════ SCROLL ══════════════════════ -->
    <div class="scroll-bar">
      <span class="scroll-label">SCROLL</span>
      <span class="scroll-sep">|</span>
    </div>

  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ArrowRight, Menu, X } from 'lucide-vue-next'
import ShinyText from './ShinyText.vue'

const videoUrl =
  'https://d8j0ntlcm91z4.cloudfront.net/user_38xzZboKViGWJOttwIXH07lWA1P/hf_20260328_105406_16f4600d-7a92-4292-b96e-b19156c7830a.mp4'

const mobileMenuOpen = ref(false)

const navLinks = [
  { label: 'Inicio',         href: '#', active: true  },
  { label: 'Sobre nosotros', href: '#'               },
  { label: 'Cursos',         href: '#'               },
  { label: 'Instructores',   href: '#'               },
  { label: 'Testimonios',    href: '#'               },
  { label: 'Contáctanos',    href: '#'               },
]
</script>

<style scoped>
/* ─── Reset & base ─── */
* { box-sizing: border-box; margin: 0; padding: 0; }

.page-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background: #111;
  font-family: 'Inter', sans-serif;
  color: #fff;
}

/* ─── NAVBAR ─── */
.navbar {
  position: relative;
  z-index: 20;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 48px;
  height: 60px;
  background: #111;
  border-bottom: 1px solid rgba(255,255,255,0.08);
  flex-shrink: 0;
}

.nav-logo {
  font-size: 17px;
  font-weight: 700;
  color: #fff;
  text-decoration: none;
  letter-spacing: -0.3px;
  white-space: nowrap;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 8px;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}

.nav-link {
  font-size: 14px;
  font-weight: 400;
  color: rgba(255,255,255,0.5);
  text-decoration: none;
  padding: 6px 14px;
  border-radius: 999px;
  transition: color 0.2s, background 0.2s;
  white-space: nowrap;
}
.nav-link:hover { color: rgba(255,255,255,0.9); background: rgba(255,255,255,0.06); }
.nav-link--active { color: #fff; font-weight: 500; }

.nav-cta {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: #fff;
  color: #000;
  font-size: 14px;
  font-weight: 600;
  padding: 10px 20px;
  border-radius: 999px;
  text-decoration: none;
  transition: background 0.2s, transform 0.2s;
}
.nav-cta:hover { background: rgba(255,255,255,0.88); transform: scale(1.02); }

.hamburger {
  display: none;
  background: none;
  border: none;
  color: rgba(255,255,255,0.8);
  cursor: pointer;
}

/* ─── MOBILE MENU ─── */
.mobile-menu {
  position: relative;
  z-index: 19;
  background: #0d0d0d;
  border-bottom: 1px solid rgba(255,255,255,0.06);
  display: flex;
  flex-direction: column;
}
.mobile-link {
  padding: 16px 24px;
  font-size: 15px;
  color: rgba(255,255,255,0.6);
  text-decoration: none;
  border-bottom: 1px solid rgba(255,255,255,0.05);
  transition: color 0.15s;
}
.mobile-link:hover { color: #fff; }

/* ─── HERO ─── */
.hero {
  position: relative;
  flex-shrink: 0;
  height: 58vh;
  min-height: 360px;
  overflow: hidden;
}

.hero-video {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero-fade-top {
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 30%;
  background: linear-gradient(to bottom, #111 0%, transparent 100%);
  pointer-events: none;
}

.hero-fade-bottom {
  position: absolute;
  bottom: 0; left: 0; right: 0;
  height: 40%;
  background: linear-gradient(to top, #151515 0%, transparent 100%);
  pointer-events: none;
}

/* Position: upper-center (25% padding-top of hero height) */
.hero-content {
  position: relative;
  z-index: 10;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding-top: 12%;
  padding-left: 24px;
  padding-right: 24px;
  gap: 20px;
}

.hero-heading {
  line-height: 0.88;
  letter-spacing: -0.03em;
  font-weight: 700;
}
.hero-heading__line1 {
  display: block;
  color: #fff;
  font-size: clamp(2.5rem, 6vw, 6rem);
}
.hero-heading__line2 {
  display: block;
  font-size: clamp(2.5rem, 6vw, 6rem) !important;
  line-height: 0.88 !important;
  letter-spacing: -0.03em !important;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  border: 1px solid rgba(255,255,255,0.2);
  border-radius: 999px;
  padding: 8px 18px;
  background: rgba(0,0,0,0.35);
  backdrop-filter: blur(8px);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.75);
}
.hero-badge__dot {
  display: inline-block;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #64CEFB;
  flex-shrink: 0;
}

.hero-cta {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  border: 1px solid rgba(255,255,255,0.3);
  border-radius: 999px;
  padding: 14px 28px;
  font-size: 15px;
  font-weight: 500;
  color: #fff;
  text-decoration: none;
  background: rgba(255,255,255,0.04);
  backdrop-filter: blur(6px);
  transition: border-color 0.25s, background 0.25s, transform 0.2s;
}
.hero-cta:hover {
  border-color: rgba(255,255,255,0.6);
  background: rgba(255,255,255,0.1);
  transform: scale(1.02);
}
.hero-cta__icon {
  transition: transform 0.25s;
}
.hero-cta:hover .hero-cta__icon {
  transform: translateX(3px);
}

/* ─── INFO STRIP ─── */
.info-strip {
  display: grid;
  grid-template-columns: 1fr 2fr 2fr 1fr;
  background: #151515;
  border-top: 1px solid rgba(255,255,255,0.1);
}

.info-col {
  padding: 56px 40px;
  border-right: 1px solid rgba(255,255,255,0.1);
}
.info-col:last-child { border-right: none; }
.info-col--empty { /* purposely empty */ }

.info-text {
  font-size: 14px;
  line-height: 1.7;
  color: rgba(255,255,255,0.6);
}

/* ─── SCROLL ─── */
.scroll-bar {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  background: #111;
  border-top: 1px solid rgba(255,255,255,0.08);
  padding: 14px;
}
.scroll-label {
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.15em;
  color: rgba(255,255,255,0.25);
}
.scroll-sep {
  color: rgba(255,255,255,0.15);
  font-size: 13px;
}

/* ─── TRANSITIONS ─── */
.slide-down-enter-active, .slide-down-leave-active { transition: all 0.22s ease; }
.slide-down-enter-from, .slide-down-leave-to { opacity: 0; transform: translateY(-8px); }

/* ─── RESPONSIVE ─── */
@media (max-width: 1024px) {
  .nav-links { display: none; }
  .nav-cta { display: none; }
  .hamburger { display: flex; }
  .navbar { padding: 0 24px; }
  .info-strip { grid-template-columns: 1fr 1fr; }
  .info-col--empty { display: none; }
  .info-col { padding: 40px 28px; }
}

@media (max-width: 640px) {
  .info-strip { grid-template-columns: 1fr; }
  .info-col { border-right: none; border-bottom: 1px solid rgba(255,255,255,0.1); }
  .info-col:last-child { border-bottom: none; }
  .hero-content { padding-top: 12%; }
}
</style>
