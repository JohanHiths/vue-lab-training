<script>
import WorkOutForm from './components/WorkOutForm.vue';
import NavbarView from './views/NavbarView.vue';
import StatisticsView from './views/StatisticsView.vue';

export default {
  components: {
    NavbarView,
    WorkOutForm,
    StatisticsView
  },

  data() {
    return {
      newName: '',
      newType: '',
      newDuration: '',
      newDifficulty: '',
      selectedFilter: 'all',
      exercises: [
        {
          id: 1,
          name: 'GYM',
          type: 'Push workout',
          duration: '30',
          difficulty: 'easy',
          completed: false,
          prio: false
        },
        {
          id: 2,
          name: 'GYM',
          type: 'Yoga',
          duration: '60',
          difficulty: 'medium',
          completed: false,
          prio: false
        },
        {
          id: 3,
          name: 'Gym',
          type: 'Running',
          duration: '90',
          difficulty: 'hard',
          completed: false,
          prio: false

        },
        {
          id: 4,
           name: 'Swimming',
          type: 'swimming',
           duration: 30,
           difficulty: 'easy',
         completed: false,
         prio: false
}
      ],
      nextExerciseId: 4
    };
  },

  methods: {
    addExercise(exercise) {
      this.exercises.push({
        id: this.nextExerciseId++,
        name: exercise.name,
        type: exercise.type,
        duration: exercise.duration,
        difficulty: exercise.difficulty,
        completed: false,
        prio: false
      });
    },
    deleteExercise(id) {
      this.exercises.splice(id, 1);
    },
    changeExercise(exercise) {
      exercise.prio = !exercise.prio;
    },
    filterWorkouts(filter) {
      this.selectedFilter = filter;
    },
    saveEdit() {
  this.$emit('edit-exercise', {
    id: this.editingExerciseId,
    name: this.newName,
    type: this.newType,
    duration: this.newDuration,
    difficulty: this.newDifficulty
  })

  this.editingExerciseId = null
},
editExercise(updatedExercise) {
  const exercise = this.exercises.find(
    (exercise) => exercise.id === updatedExercise.id
  )

  exercise.name = updatedExercise.name
  exercise.type = updatedExercise.type
  exercise.duration = updatedExercise.duration
  exercise.difficulty = updatedExercise.difficulty
}
  }
};
</script>
<template>
  
  <div class="app">
     <NavbarView @filter-workouts="filterWorkouts" />
    <WorkOutForm
  :exercises="exercises"
  :selected-filter="selectedFilter"
  @add-exercise="addExercise"
  @delete-exercise="deleteExercise"
  @edit-exercise="editExercise"
/>
    
    
  </div>
  <StatisticsView :exercises="exercises" />
  <p>Current filter: {{ selectedFilter }}</p>
</template>

<style scoped>


.app {
    display:grid;
  grid-template-columns: 1fr 2fr -1fr 2;
}




</style>
