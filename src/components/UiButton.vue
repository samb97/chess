<script setup lang="ts"></script>

<template>
  <button
    type="button"
  >
    <slot />
  </button>
</template>

<style scoped>
button {
  @apply py-4 px-6 leading-tight rounded-full bg-blue-800 text-white uppercase font-semibold;
}
</style>