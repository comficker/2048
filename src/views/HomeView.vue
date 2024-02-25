<template>
  <div class="container">
    <div class="board" tabIndex="1">
      <div v-for="(r_item, r_i) in board.cells" :key="r_i">
        <cell v-for="(c_item, c_i) in r_item" :key="c_i"/>
      </div>
      <tile-view v-for="(tile, i) in tiles" :tile="tile" :key="i"/>
      <game-end-overlay :board="board" :onrestart="onRestart"/>
    </div>
  </div>
</template>

<script lang="ts">
import Cell from "@/components/Cell.vue";
import TileView from "@/components/TileView.vue";
import GameEndOverlay from "@/components/GameEndOverlay.vue";
import {Board} from "@/board";
import {onMounted, onBeforeUnmount, ref, computed} from "vue";

export default {
  setup() {
    // @ts-ignore
    const board = ref(new Board());
    // @ts-ignore
    const handleKeyDown = (event) => {
      if (board.value.hasWon()) {
        return;
      }
      if (event.keyCode >= 37 && event.keyCode <= 40) {
        event.preventDefault();
        const direction = event.keyCode - 37;
        board.value.move(direction);
      }
    };
    const onRestart = () => {
      // @ts-ignore
      board.value = new Board();
    };
    onMounted(() => {
      window.addEventListener("keydown", handleKeyDown);
    });
    onBeforeUnmount(() => {
      window.removeEventListener("keydown", handleKeyDown);
    });
    const tiles = computed(() => {
      // @ts-ignore
      return board.value.tiles.filter((tile) => tile.value !== 0);
    });
    return {
      board,
      onRestart,
      tiles,
    };
  },
  components: {
    Cell,
    TileView,
    GameEndOverlay,
  },
};
</script>

<style>
.container {
  display: flex;
  align-items: center;
  align-content: center;
  justify-items: center;
  min-height: 75vh;
}
</style>
