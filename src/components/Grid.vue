<script setup lang="ts">
import { ref } from "vue"

const buildGrid = (size: number) => {
  return [...Array(size)].map((_) => [...Array(size)].map((_) => [...Array(size)].map((_) => [...Array(size)].map((_) => "x"))))
}
const gridVals = ref(buildGrid(3))

function solve() {
  // TODO: call an API to solve the Sudoku included in gridVals
  // TODO (low priority): make the Sudoku's dimensions flexible, to allow solving 4x4, 9x9 or even 16x16 grids
  console.log(gridVals.value)
}
</script>

<template>
  <div class="mx-auto table border-2 border-gray-800 rounded-sm">
    <table class="flex flex-row" v-for="(blockLine, idBlLine) in gridVals" v-bind:key="blockLine">
      <table class="border-2 border-gray-800" v-for="(block, idBl) in blockLine" v-bind:key="block">
        <tr v-for="(line, idLine) in block" v-bind:key="line" class="flex flex-row">
          <td v-for="(elem, idElem) in line" v-bind:key="elem" class="border border-gray-300">
            <input
              v-model="gridVals[idBlLine][idBl][idLine][idElem]"
              class="w-6 h-6 text-center"
              type="text"
              required
              pattern="[x1-9]{1}"
            />
          </td>
        </tr>
      </table>
    </table>
  </div>

  <button class="w-64 border-2 border-gray-500 rounded-sm mx-auto my-4" @click="solve">SOLVE</button>
</template>

<style scoped>
input:invalid {
  background: #df8686;
}
</style>
