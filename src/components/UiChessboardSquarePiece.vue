<script setup lang="ts">
import { computed } from 'vue';
import { Color, PieceSymbol } from 'chess.js'
import SvgBishop from '../assets/pieces/bishop.svg?component';
import SvgKnight from '../assets/pieces/knight.svg?component';
import SvgPawn from '../assets/pieces/pawn.svg?component';
import SvgKing from '../assets/pieces/king.svg?component';
import SvgQueen from '../assets/pieces/queen.svg?component';
import SvgRook from '../assets/pieces/rook.svg?component';

const props = defineProps<{
  piece: PieceSymbol;
  color: Color;
}>()

const pieceMap = {
  b: SvgBishop,
  n: SvgKnight,
  p: SvgPawn,
  k: SvgKing,
  q: SvgQueen,
  r: SvgRook,
}

const componentPiece = computed(() => {
  const { piece } = props
  return pieceMap[piece]
})
</script>


<template>
  <component
    :is="componentPiece"
    class="w-full h-full p-1 select-none"
    :class="[
      {'fill-white': props.color === 'w'},
      {'fill-black': props.color === 'b'},
    ]"
  />
</template>