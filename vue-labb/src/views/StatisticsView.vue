<script>
export default {
  data() {
    return {
    newName: '',
    newType: '',
    newDuration: '',
    newDifficulty: '',
    
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
                }
            ],
      nextExerciseId: 4
    }
  },
  methods: {
      addExercise(){
        this.exercises.push({
          id: this.nextExerciseId++,
          name: this.newName,
          type: this.newType,
          duration: this.newDuration,
          difficulty: this.newDifficulty,
          completed: false,
          prio: false
        } )
        this.newExercise = ''
      },
      deleteExercise(id){
        this.exercises.splice(id, 1)
      },
      changeExercise(exercise){
        if (exercise.prio === true) {
      exercise.prio = false
      } else {
      exercise.prio = true

        
    }
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

.workout-statistics{
  display: flex;
  flex-direction: column;
  min-height: 200px;
  width:500px;
  margin: 0 auto;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 2rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
  overflow:visible;
  margin-left:15px;
}

</style>
