<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/" class="button"><h1 >Home</h1></RouterLink>
        <RouterLink to="/about"><h1>About</h1></RouterLink>
      </nav>
    </div>
  </header>

  <RouterView class="view" />
</template>

<style scoped>
h1 {
  display: inline-block;
  padding-right: 10px;
  padding-left: 10px;
}

header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;
  padding-left: 20px;
  padding-top: 15px;
  padding-bottom: 15px;
  background-color: var(--vt-c-black-mute);
}

.logo:hover {
  cursor: pointer;
}

.logo {
  background: -webkit-linear-gradient(
      0.5turn,
      rgba(135, 240, 252, 1),
      rgba(191, 120, 251, 1),
      rgba(250, 115, 198, 1));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

span {
  color: var(--v-info-base);
}

.icon {
  filter: grayscale(1);
  width: 2em;
  transition: 0.5s;
}

.button.active .icon {
  filter: grayscale(0);
}

.button.active {
  opacity: 1 !important;
}

.button:hover .icon {
  filter: grayscale(0);
}

.underlineEffect {
  display: inline-block;
}

.button:hover .underlineEffect::before {
  transform: scaleX(1);
}

.active .underlineEffect::before {
  transform: scaleX(1) !important;
}

.underlineEffect::before {
  content: '';
  position: absolute;
  width: 100%;
  height: 4px;
  border-radius: 2px;
  bottom: -10px;
  left: 0;
  background: -webkit-linear-gradient(
      1turn,
      rgba(135, 240, 252, 1),
      rgba(191, 120, 251, 1),
      rgba(250, 115, 198, 1));
  transform-origin: bottom left;
  transition: transform 0.4s ease-out;
  transform: scaleX(0);
}

.v-btn {
  opacity: 0.85 !important;
}

</style>
