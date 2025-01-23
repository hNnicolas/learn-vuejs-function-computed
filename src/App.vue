<template>
  <input type="number" v-model="product.quantity" />
  <input type="number" v-model="price" />
  <h2>Prix total HT : {{ totalPriceHT }}</h2>
  <h2>Prix total TTC : {{ totalPriceTTC }}</h2>
</template>

<script setup lang="ts">
import { computed, reactive, ref, watch, watchEffect } from 'vue'

interface Product {
  name: string
  quantity: number
  priceHT: number
  nbrOfModification: number
  lastModification?: number
}

const product =
  reactive <
  Product({
    name: 'books',
    quantity: 3,
    priceHT: 10,
    nbrOfModification: 0,
  })

const price = ref(0)

const totalPriceHT = computed(() => product.priceHT * product.quantity)
const totalPriceTTC = computed(() => product.priceHT * product.quantity * 1.2)

const unwatch = watch([() => product.quantity, price], (newValue, oldValue) => {
  product.nbrOfModification++
  console.log(newValue)
  console.log(oldValue)
})

setTimeout(() => {
  const mywatchEffect = watchEffect(() => {
    console.log('in watchEffect')
    product.priceHT = price.value
    product.lastModification = Date.now()
    console.log(product)
  })
})
</script>

<style></style>
