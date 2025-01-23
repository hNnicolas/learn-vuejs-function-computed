<template>
  <h2>Prix total HT : {{ totalPriceHT }}</h2>
  <h2>Prix total TTC : {{ totalPriceTTC }}</h2>
</template>

<script setup lang="ts">
import { computed, reactive } from 'vue'

const product = reactive({
  name: 'books',
  quantity: 3,
  priceHT: 10,
})

const totalPriceHT = computed(() => product.totalPriceHT * product.quantity)
const totalPriceTTC = computed(() => product.totalPriceHT * product.quantity * 1.2)
</script>

<style></style>
