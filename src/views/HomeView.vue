<script setup>

import TitleSection from '../components/Home/TitleSection.vue'
import PopularSection from '../components/Home/PopularSection.vue'
import { ref, onMounted } from 'vue'
import { supabase } from '../lib/supabaseClient'

const products = ref([])
async function getInstruments() {
  const { data } = await supabase.from('products').select()
  products.value = data
}
onMounted(() => {
  getInstruments()
})

</script>

<template>
  <!-- Hero Section -->
  <TitleSection />

  <!-- Produits en vedette -->
  <PopularSection />

  <ul>
    <li v-for="product in products" :key="product.id">{{ product.name }}</li>
  </ul>
</template>
