<script>
export default {
  data() {
    return {
    newExercise: '',
    newExerciseName: '',
    newExerciseType: '',
    newExerciseDuration: '',
    newExerciseDifficulty: '',
    newExerciseCompleted: '',
    
    exercises: [
                {
        id: 1,
        name: 'GYM',
        type: 'Push workout',
		    duration: '20',
	      difficulty: 'easy',
	      completed:"NO"
        },
       {
        id: 2,
        name: 'GYM',
        type: 'Yoga',
        duration: '60',
	      difficulty: 'medium',
	      completed:"ON HOLD"
                    
                },
                {
        id: 3,
        name: 'Gym',
        type: 'Running',
		    duration: '10',
	            difficulty: 'hard',
	            completed:"YES"                   
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
          completed: this.newCompleted
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
     <div class="container">
    <p>Add a Workout:</p>
    <form @submit.prevent="addExercise">
      <input v-model="newName" type="text" placeholder="Workout Name" />
      <input v-model="newType" type="text" placeholder="Workout Type" />
      <input v-model="newDuration" type="text" placeholder="Workout Duration" />
      
      <select>  
        <option value="">Select Difficulty</option>
        <option class="easy" value="easy">Easy</option>
        <option class="medium" value="medium">Medium</option>
        <option class="hard" value="hard">Hard</option>
      </select>
      <button v-if="newExercise > 0" class="workout-btn">Add Workout</button>
      </form>
        <ul>
    <li v-for="(exercise, index) in exercises" :key="exercise.id" :class="{prio: exercise.prio}">
        {{exercise.id}} {{exercise.name}}
        <button @click="deleteExercise(index)">Ta bort</button>
        <button @click="changeExercise(exercise)">Ändra prio</button>
    </li>
</ul>
      </div>
</template>

<style>

.container{
  display: flex;
  flex-direction: column;
  height: 500px;
  width:500px;
  margin: 0 auto;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 2rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}
p{
  font-size: 1.2rem;
  color: #333;
}

input{
  margin: 0.5rem 0;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: calc(100% - 1rem);
}

button.workout-btn{
  align-self: center;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: #35b835;
  color: white;
  cursor: pointer;
  width:300px;
}

select{
  margin: 0.5rem 0;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: calc(100% - 1rem);
}
.easy{
    color:rgb(15, 122, 15);
}

.medium{
    color:rgb(202, 143, 88);
}

.hard{
    color:red;
}
</style>