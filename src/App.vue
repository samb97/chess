<script setup lang="ts">
import { ref } from 'vue';
import UiButton from './components/UiButton.vue'
import UiChessboard from './components/UiChessboard.vue'

const isBoardFlipped = ref(false)
console.log("🚀 ~ file: App.vue ~ line 7 ~ isBoardFlipped", isBoardFlipped)

function flipBoard() {
  isBoardFlipped.value = !isBoardFlipped.value;
}
</script>

<template>
  <UiChessboard :is-flipped="isBoardFlipped" />
  
  <div>
    <h1>ACTIONS</h1>
    <div class="flex flex-wrap gap-4">
      <UiButton @click="flipBoard">
        FLIP BOARD
      </UiButton>
    </div>
  </div>
</template>