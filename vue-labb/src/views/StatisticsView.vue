<script>
export default {
  props: {
    exercises: {
      type: Array,
      required: true
    }
  }
}
</script>
<template>
  <div class="workout-statistics">
  <h1>Workout Statistics📈📊</h1>
    <span class="statistic-span">Total workouts {{ exercises.length }}</span>
    <span class="statistic-span">Completed workouts {{ exercises.filter((exercises) => exercises.completed).length }}</span>
    <span class="statistic-span">Remaining workouts {{ exercises.filter((exercises) => !exercises.completed).length}}</span>
    <span class="statistic-span">Total training time {{ exercises.reduce((total, exercise) => total + exercise.duration, 0) }}
  minutes</span>
    <span class="statistic-span">Remaining time⏰ {{ }}</span>

</div>
</template>

<style>

.workout-statistics {
  display: flex;
  flex-direction: column;
  height: 400px;
  width: 400px;
  margin: 0 auto;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 2rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
  overflow: visible;
  margin-left:200px;
  }

</style>
