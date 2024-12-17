<script setup lang="ts">
import { useRoute, useRouter } from 'vue-router';
import data_people from '@/data/data_people';
import { computed } from 'vue';

const route = useRoute();
const router = useRouter();

const personId = Number(route.params.id);
const person = computed(() => data_people.getPeople().find(p => p.id === personId));

function goBack() {
  router.back();
}
</script>

<template>
  <div v-if="person" class="contact-view">
    <button @click="goBack" class="btn btn-outline-primary mb-3">Vissza</button>
    <div class="card mx-auto" style="width: 20rem;">
      <img :src="person.avatar" class="card-img-top" :alt="`${person.first_name} ${person.last_name}`" />
      <div class="card-body text-center">
        <h3 class="card-title">{{ person.first_name }} {{ person.last_name }}</h3>
        <p class="card-text">Email: {{ person.email }}</p>
      </div>
    </div>
  </div>
  <div v-else>
    <p class="text-danger">Nincs ilyen személy.</p>
  </div>
</template>

<style scoped>
.contact-view {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
}
</style>
