<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/list">List View</RouterLink>
    </nav>
  </header>

  <main>
    <RouterView v-slot="{ Component }">
      <Transition name="slide">
        <component :is="Component" />
      </Transition>
    </RouterView>
  </main>
</template>

<style scoped>
nav {
  display: flex;
  justify-content: center;
  gap: 20px;
  padding: 20px;
}

nav a {
  text-decoration: none;
  color: var(--color-text);
  font-family: Resist Bold;
  font-size: 30px;
}

main {
  display: flex;
  justify-content: center;
  align-items: center;
}

.wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.slide-enter-active,
.slide-leave-active {
  transition: all 0.75s ease-out;
}

.slide-enter-to {
  position: absolute;
  right: 0;
}

.slide-enter-from {
  position: absolute;
  right: -100%;
}

.slide-leave-to {
  position: absolute;
  left: -100%;
}

.slide-leave-from {
  position: absolute;
  left: 0;
}

@font-face {
  font-family: Resist;
  src: url('@/assets/fonts/resistsans-txtlight-webfont.woff');
}

@font-face {
  font-family: Resist Bold;
  src: url('@/assets/fonts/resistsans-dsplmediumoblique-webfont.woff');
}
</style>
