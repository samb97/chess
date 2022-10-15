<script setup lang="ts">
import { Square, PieceSymbol, Color } from 'chess.js'
import UiChessboardSquarePiece from './UiChessboardSquarePiece.vue';

const props = defineProps<{
  square: {
    square: Square,
    type: PieceSymbol,
    color: Color,
  } | null;
  mayExpectAPiece?: boolean;
}>()

const emit = defineEmits<{
  (e: 'click'): void
}>()
</script>


<template>
  <div
    class="p-2 relative flex items-center justify-center"
    :class="{ 'cursor-pointer': square?.type }"

    @click="emit('click')"
  >
    <span v-if="props.square" class="absolute top-2 left-2">
      {{ props.square.square }}
    </span>
    <div v-if="props.mayExpectAPiece" class="w-1/3 h-1/3 absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 rounded-full bg-gray-800"></div>
    <UiChessboardSquarePiece
      v-if="square"
      
      :piece="square.type"
      :color="square.color"
    />
  </div>
</template>