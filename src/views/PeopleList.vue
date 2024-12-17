<script setup lang="ts">
import PeopleCard from '@/components/PeopleCard.vue';
import data_people from '@/data/data_people';
import type People from '@/types/People';
import { ref } from 'vue';

const people = ref<People[]>(data_people.getPeople());

const sortOrder = ref<'asc' | 'desc'>('asc');

function sortPeople(order: 'asc' | 'desc') {
  sortOrder.value = order;
  people.value.sort((a, b) => {
    const nameA = `${a.first_name} ${a.last_name}`.toLowerCase();
    const nameB = `${b.first_name} ${b.last_name}`.toLowerCase();
    return order === 'asc' ? nameA.localeCompare(nameB) : nameB.localeCompare(nameA);
  });
}

sortPeople("asc")
</script>

<template>
  <div>
    <h1 class="display-5">Emberek</h1>
    <div class="mb-3">
      <button @click="sortPeople('asc')" class="btn btn-primary me-2">Rendezés: A-Z</button>
      <button @click="sortPeople('desc')" class="btn btn-secondary">Rendezés: Z-A</button>
    </div>
    <div class="people-list">
      <PeopleCard
        v-for="person in people"
        :key="person.id"
        :id="person.id"
        :first_name="person.first_name"
        :last_name="person.last_name"
        :email="person.email"
        :avatar="person.avatar"
      />
    </div>
  </div>
</template>

<style scoped>
.people-list {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}
</style>
