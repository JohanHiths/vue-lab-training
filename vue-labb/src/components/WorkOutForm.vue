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
		    duration: '20',
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
		    duration: '10',
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
     <div class="container">
    <p>Add a Workout:</p>
    <form @submit.prevent="addExercise">
      <input v-model="newName" type="text" placeholder="Workout Name" />
      <input v-model.number="newDuration" type="number" placeholder="Workout Duration" />
      <select v-model="newDifficulty">  
        <option value="">Select Difficulty</option>
        <option class="easy" value="easy">Easy</option>
        <option class="medium" value="medium">Medium</option>
        <option class="hard" value="hard">Hard</option>
      </select>
      <select v-model="newType">
      <option value="">Select Workout Type</option>
      <option value="strength">Strength💪</option>
       <option value="cardio">Cardio🏃</option>
      <option value="yoga">Yoga🧘🏻‍♀️</option>
      <option value="mobility">Mobility🤸🏻</option>
      </select>
       <p>Workout List</p>
      <button v-if="newName.length > 0" class="workout-btn">Add Workout</button>
      </form>
        <ul>
    <li v-for="(exercise, index) in exercises" :key="exercise.id" :class="{prio: exercise.prio}">
        {{exercise.id}} {{exercise.name}} {{ exercise.type }} {{ exercise.duration }} min {{ exercise.difficulty }}
        <button class="remove-btn" @click="deleteExercise(index)">Remove</button>
        <button class="change-btn" @click="changeExercise(exercise)">Change</button>
        <span @click="exercise.completed = !exercise.completed" v-if="exercise.completed">✓ Completed</span>
        <span @click="exercise.completed = !exercise.completed" v-else>✗ Not completed</span>
    </li>
</ul>
      </div>
</template>

<style>

.container{
  display: flex;
  flex-direction: column;
  min-height: 500px;
  width:500px;
  margin: 0 auto;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 2rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
  overflow:visible;
  
}
p{
  font-size: 20px;
  color: #333;
}

input{
  margin: 0.5rem 0;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: calc(100% - 1rem);
}

 .workout-btn{
  align-self: center;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: #252d9c;
  color: white;
  cursor: pointer;
  width:300px;
}

.change-btn{
  align-self: center;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: #35b835;
  color: white;
  cursor: pointer;
  width:100px;
}
.remove-btn{
  align-self: center;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: #d44431;
  color: white;
  cursor: pointer;
  width:100px;
  margin-right:10px;
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

li{
  list-style-type: none;
}
</style>