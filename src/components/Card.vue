<template>
    <v-card class="w-100 h-100 d-flex flex-column mr-0">
        <v-img class="align-end text-white" height="200" :src="card.images[0]" cover>
        </v-img>
        <v-card-title>{{ card.title }}</v-card-title>
        <v-card-text>
            <div class="card-description">{{ card.description }}</div>
        </v-card-text>

        <v-card-actions>
            <v-chip>
                <strong>{{ card.price }} $</strong>
            </v-chip>
        </v-card-actions>
    </v-card>
</template>
  
<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    card: {
        type: Object,
        required: true,
    },
});
</script>

<style>
.card-description {
    height: 80px;
    overflow: auto;
}
</style>
  