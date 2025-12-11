<script setup lang="ts">
import { ref, computed } from 'vue'

interface Plate {
  id: number
  name: string
  price: number
  count: number
  color?: string
  custom?: boolean
}

const plates = ref<Plate[]>([
  { id: 1, name: '粉色盤', price: 30, count: 0, color: 'text-[#F2AEA4]' },
  { id: 2, name: '灰色盤', price: 40, count: 0, color: 'text-[#C3C4D2]' },
  { id: 3, name: '黑色盤', price: 60, count: 0, color: 'text-[#4A4646]' },
  { id: 4, name: '其他', price: 1, count: 0, custom: true },
])

const totalPrice = computed(() => {
  return plates.value.reduce((sum, plate) => sum + plate.price * plate.count, 0).toLocaleString()
})

</script>

<template>
  <div class="bg-[#EA9970] font-bold text-white p-4">爭鮮計算機</div>
  <div class="w-[85%] max-w-[500px] mx-auto my-10 flex flex-col gap-5">
    <div v-for="plate in plates" :key="plate.id" class="flex items-center justify-between">

      <div class="flex items-center gap-5">
        <i v-if="!plate.custom" :class="plate.color" class="fi fi-sr-plate text-[54px] leading-none"></i>
        <i v-else class="fi fi-ss-bowl-chopsticks text-[54px] leading-none text-[#EA9970]"></i>

        <div class="text-center w-[50px]">
          <div class="font-bold text-[#4A4A4A]">{{ plate.name }}</div>
          <div v-if="!plate.custom" class="text-[#9D9D9D] font-bold text-sm">${{ plate.price }}</div>
        </div>
      </div>

      <label>
        <input type="number" min="0" step="1" class="w-16 p-1 text-center text-[#4A4A4A] border border-[#4A4A4A] rounded"
           v-model.number="plate.count" />
      </label>
    </div>

    <hr class="text-[#4A4A4A]">

    <div class="mt-6 text-right font-bold">
      <span class="text-sm text-[#4A4A4A]">總計</span> <span class="text-[#EA9970] text-xl">＄{{ totalPrice }} </span>
    </div>
  </div>

</template>

<style>
@import "tailwindcss";
</style>