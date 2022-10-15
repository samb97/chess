<script setup lang="ts">
import { Chess, Square, Move } from 'chess.js'
import { computed, ref, watch } from 'vue';
import UiChessboardSquare from './UiChessboardSquare.vue'

const props = withDefaults(defineProps<{
  size?: number;
  isFlipped: boolean;
}>(), {
  size: 800,
  isFlipped: false,
})
const chess = new Chess()
const targetSquare = ref<Square | undefined>();
const validMoves = computed(() => {
  return chess.moves({
    square: targetSquare.value,
    verbose: true,
  })
})
const validSquares = computed<Square[]>(() => {
  return validMoves.value.map((move: any) => move.to)
})

function handleSquareClicked(square?: Square) {
  if (targetSquare.value === undefined) {
    targetSquare.value = square
    return
  }

  chess.move({ from: targetSquare.value, to: square })
  targetSquare.value = undefined;
}

function algebraicSquare(row: number, col: number): Square {
  let a = '';
  let b = '';

  if (col === 0) {
    a = 'a';
  }

  if (col === 1) {
    a = 'b';
  }

  if (col === 2) {
    a = 'c';
  }

  if (col === 3) {
    a = 'd';
  }

  if (col === 4) {
    a = 'e';
  }

  if (col === 5) {
    a = 'f';
  }

  if (col === 6) {
    a = 'g';
  }

  if (col === 7) {
    a = 'h';
  }

  b = String(8 - row);

  return `${a}${b}` as Square
}

window.addEventListener('keydown', (event) => {
  if (event.key === "Escape") {
    targetSquare.value = undefined;
  }
})
</script>

<template>
  <div
    class="grid grid-rows-8 auto-rows-fr select-none"
    :class="[
      {'transform rotate-180': props.isFlipped}
    ]"
    :style="{
      width: `${props.size}px`,
      height: `${props.size}px`,
    }"
  >
    <div
      v-for="(row, rowIndex) in chess.board()"
      :key="`chess-row--${rowIndex}`"

      class="grid grid-cols-8 auto-rows-fr"
    >
      <UiChessboardSquare
        v-for="(square, squareIndex) in row"
        :key="`chess-square--${squareIndex}`"

        :class="[
          { 'bg-gray-400': squareIndex % 2 === rowIndex % 2 },
          { 'bg-gray-600': squareIndex % 2 !== rowIndex % 2 },
        ]"

        :square="square"
        :may-expect-a-piece="targetSquare !== undefined &&  validSquares.includes(algebraicSquare(rowIndex, squareIndex))"

        @click="handleSquareClicked(algebraicSquare(rowIndex, squareIndex))"
      />
    </div>
  </div>
</template>
