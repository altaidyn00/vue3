<template>
  <div class="cards-view">
    <h1 class="text-center mb-10">Products</h1>
    <div v-if="isLoading" class="loader">
      <v-progress-circular :size="75" color="primary" indeterminate></v-progress-circular>
    </div>
    <div v-else class="cards">
      <div v-for="(card, index) in products" :key="'card_' + index" class="card--wrapper">
        <Card :card="card" />
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref, computed } from 'vue'
import axios from 'axios'
import Card from '../components/Card.vue'

export default {
  name: 'CardsView',
  components: {
    Card,
  },
  setup() {
    const cards = ref([])
    const apiUrl = 'https://dummyjson.com/products'
    const data = ref(null)
    const isLoading = ref(true)

    onMounted(async () => {
      try {
        isLoading.value = true
        data.value = await axios.get(apiUrl).then((response) => {
          cards.value = response.data;
        });
      } catch (error) {
        console.log(error)
      } finally {
        isLoading.value = false
      }
    });

    const products = computed(() => {
      return cards?.value?.products;
    })

    return { products, isLoading };
  }
}
</script>

<style scoped>
.cards-view {
  max-width: 1200px;
  min-height: 100vh;
  padding: 120px 20px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.cards {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}

.card--wrapper {
  width: 31%;
  height: 400px;
  margin-bottom: 40px;
}

.loader {
  margin: auto;
}

@media screen and (max-width: 768px) {
  .card--wrapper {
    width: 48%;
  }
}

@media screen and (max-width: 480px) {
  .cards {
    width: 100%;
  }

  .card--wrapper {
    width: 100%;
  }
}
</style>
