<script setup>
import { RouterLink, RouterView } from 'vue-router'
import WorkoutForm from './components/WorkOutForm.vue'
import StatisticsView from './views/StatisticsView.vue';
import NavbarView from './views/NavbarView.vue';



</script>
<template>
  <div class="app">

    <NavbarView />

    <div class="widgets">
      <WorkoutForm />
      <StatisticsView />
    </div>

  </div>
</template>


<style scoped>
.app {
  text-align: center;
}

.widgets {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}

</style>
