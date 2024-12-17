<script setup lang="ts">
import { useRouter } from 'vue-router';

const props = defineProps<{
  id: number;
  first_name: string;
  last_name: string;
  email: string;
  avatar: string;
}>();

const router = useRouter();

function navigateToContact() {
  router.push(`/keszitette/${props.id}`);
}
</script>

<template>
  <div class="card" style="width: 18rem;">
    <img
      :src="avatar"
      class="card-img-top"
      :alt="`${first_name} ${last_name}`"
      style="cursor: pointer;"
      @click="navigateToContact"
    />
    <div class="card-body">
      <h5 class="card-title" style="cursor: pointer;" @click="navigateToContact">
        {{ first_name }} {{ last_name }}
      </h5>
      <p class="card-text">{{ email }}</p>
    </div>
  </div>
</template>

<style scoped>
.card {
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}
.card:hover {
  transform: scale(1.05);
}
</style>
