<script>
export default {
  props: {
    exercises: {
      type: Array,
      required: true
    },
     selectedFilter: {
    type: String,
    required: true
  }
  },

  data() {
    return {
      search: '',
      editingExerciseId: null,
      newName: '',
      newType: '',
      newDuration: '',
      newDifficulty: ''
    }
  },
 computed: {
  filteredExercises() {

    let workouts = this.exercises

    if (this.selectedFilter !== 'all') {
      workouts = workouts.filter((exercise) => {
        return exercise.type === this.selectedFilter
      })
    }

    if (this.search) {
      workouts = workouts.filter((exercise) => {
        return exercise.name
          .toLowerCase()
          .includes(this.search.toLowerCase())
      })
    }

    return workouts
  }
},
  methods: {
    addExercise() {
      this.$emit('add-exercise', {
        name: this.newName,
        type: this.newType,
        type: this.swimming,
        duration: this.newDuration,
        difficulty: this.newDifficulty
      })
    },
    deleteExercise(id) {
        this.exercises.splice(id, 1)
    },
    changeExercise(exercise) {
      if (exercise.prio === true) {
        exercise.prio = false
      } else {
        exercise.prio = true
      }
    }
  },
  startEditing(exercise) {
  this.editingExerciseId = exercise.id

  this.newName = exercise.name
  this.newType = exercise.type
  this.newDuration = exercise.duration
  this.newDifficulty = exercise.difficulty
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




</script>

<template>
  
  <div class="grid">
    
     <div class="container">
      
    <p class="workout-search">Search for a workout</p>
    <input class="search-workout" type="text" v-model="search" placeholder="search workouts" />
    

    <p class="workout">Add a Workout:</p>
    
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
      <option value="mobility">Climbing🧗</option>
      <option value="swimming">Swimming🏊</option>

      </select>

      

       <p>Workout List</p>
       
       <p v-if="exercises.length === 0">
        No workouts yet 🏋️
        Add your first workout above!
      </p>
    <button
  v-if="editingExerciseId === null && newName.length > 0"
  class="workout-btn"
  @click="addExercise"
>
  Add Workout
</button>
<button
  v-if="editingExerciseId !== null"
  class="workout-btn"
  @click="saveEdit"
>
  Save Changes
</button>
      
      </form>
        <ul>
    <li
  v-for="(exercise, index) in filteredExercises"
  :key="exercise.id"
>
  <div class="workout-info">
    <strong>{{ exercise.id }}. {{ exercise.name }}</strong>
    <span>{{ exercise.type }}</span>
    <span>{{ exercise.duration }} min</span>
    <span>{{ exercise.difficulty }}</span>
      <div class="workout-actions">
    <button class="remove-btn" @click="$emit('delete-exercise', index)">  
   Remove
</button>

    <button class="change-btn" @click="$emit('change-exercise', exercise)">
      ✏️ Edit
    </button>

    <span
      @click="exercise.completed = !exercise.completed"
      v-if="exercise.completed"
    >✅ Completed   
    </span>

    <span
      @click="exercise.completed = !exercise.completed"
      v-else
    >❌ Not completed
    </span>
  </div>

    
  </div>


</li>
</ul>

</div>




</div>
</template>

<style>

.workout-search{
  font-size:25px;
}


.grid{
  display:grid;
  grid-template-columns: 1fr 1fr;


}

.workout{
  font-size:25px;
}
.statistic-span{
  font-size:20px;
  margin-top:10px;

}

.total-workouts{
  font-size:25px;
}



.container{
  display: flex;
  flex-direction: column;
  min-height: 300px;
  width:800px;
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
  margin-top:15px;
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
  display:flex;
  flex-direction:column;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: #35b835;
  color: white;
  cursor: pointer;
  width:80px;
  height:30px;
  overflow: visible;
}
.remove-btn{
  display:flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  background-color: #d44431;
  color: white;
  cursor: pointer;
  width:80px;
  height:30px;
  margin-right:10px;
  overflow: visible;
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
.workout-info {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-top: 10px;
  margin-left: 20px;
  border: 2px solid black;
  flex-wrap: nowrap;
}


span{
  margin-left:15px;
}
</style>