<script setup lang="ts">
import data from '../partners.json'
import { Partner } from './type'
import { normalizeName, track } from './utils'
import PartnerCard from './PartnerCard.vue'
import { VTIconChevronLeft } from '@vue/theme'

const { partner } = defineProps<{
  partner: string
}>()

const p = (data as Partner[]).find(
  (p) => normalizeName(p.name) === partner
)!

const { name, description, hiring, contact, website } = p

function genMailLink(email: string) {
  return `mailto:${email}?subject=Looking for a Vue.js Partner`
}
</script>

<template>
  <div class="partner-page">
    <div class="back">
      <a href="/partners/all.html"
        ><VTIconChevronLeft class="icon" />Volver a todos los socios</a
      >
    </div>

    <PartnerCard hero page :data="p" />

    <div class="description">
      <h2>Acerca de {{ name }}</h2>
      <p v-for="desc in description" v-html="desc"></p>
    </div>

    <div class="actions">
      <a :href="website.url" target="_blank" @click="track"
        >Visitar el Sitio Web</a
      >
      <a
        class="contact"
        :href="genMailLink(contact)"
        target="_blank"
        @click="track"
        >Contactar</a
      >
    </div>

    <div class="hiring" v-if="hiring">
      <a :href="hiring" @click="track">¡{{ name }} está contratando!</a>
    </div>
  </div>
</template>

<style scoped>
.partner-page {
  max-width: 1080px;
  margin: 2em auto;
  padding: 0 28px 64px;
}

.back {
  display: block;
  font-size: 0.9em;
  font-weight: 600;
  margin: 24px 0 96px;
}

.back a {
  color: var(--vt-c-text-3);
  transition: color 0.5s;
}

.back a:hover {
  color: var(--vt-c-text-2);
}

.icon {
  width: 22px;
  height: 22px;
  display: inline-block;
  fill: var(--vt-c-text-3);
  position: relative;
  top: -1px;
  margin-right: 4px;
}

.description {
  max-width: 688px;
  margin: 4em auto;
}

h2 {
  font-size: 1.8em;
  font-weight: 700;
  margin-top: 96px;
  margin-bottom: 48px;
  text-align: center;
}

.description p {
  margin-bottom: 1em;
  font-size: 17px;
  line-height: 1.6em;
  color: var(--vt-c-text-2);
}

.actions {
  text-align: center;
  margin-bottom: 24px;
}

.actions a {
  text-align: center;
  background-color: var(--vt-c-brand);
  color: var(--vt-c-bg);
  padding: 12px 24px;
  font-weight: 600;
  border-radius: 6px;
  transition: background-color 0.5s, color 0.5s;
  margin: 0 8px;
}

.actions a:hover {
  background-color: var(--vt-c-brand-dark);
}

.actions a.contact {
  color: var(--vt-c-text-code);
  background-color: var(--vt-c-bg-mute);
}

.actions a.contact:hover {
  background-color: var(--vt-c-gray-light-4);
}

.dark .actions a.contact:hover {
  background-color: var(--vt-c-gray-dark-3);
}

.hiring {
  text-align: center;
}

.hiring a {
  display: inline-block;
  font-size: 15px;
  font-weight: 500;
  color: var(--vt-c-text-2);
  border-top: 1px solid var(--vt-c-divider-light);
  margin-top: 16px;
  padding-top: 20px;
}

.hiring a:hover {
  color: var(--vt-c-green);
}

@media (max-width: 768px) {
  .back {
    margin-bottom: 48px;
  }
  h2 {
    margin-top: 48px;
  }
}
</style>
