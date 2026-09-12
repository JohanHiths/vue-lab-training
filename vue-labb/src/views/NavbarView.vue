<script>
import StatisticsView from './StatisticsView.vue';
</script>

<template>
    <nav>
  <div class="navbar">

    <button
  class="all-btn"
  @click="$emit('filter-workouts', 'all')">
  All workouts
</button>
  
  <div class="dropdown">
    <button
  class="dropbtn"
  @click="$emit('filter-workouts', 'strenght')"
> <i class="fa fa-caret-down"></i>
  Strenght
</button>
    <div class="dropdown-content">
      <a @click.prevent="$emit('filter-workouts', 'push-ups')">Push-ups</a>
      <a @click.prevent="$emit('filter-workouts', 'deadlift')">Deadlift🏋🏽‍♂️</a>
      <a @click.prevent="$emit('filter-workouts', 'benchpress')">Bench press</a>
    </div>
    
  </div> 
  <div class="dropdown">
    
    
  <button
  class="dropbtn"
  @click="$emit('filter-workouts', 'cardio')"
> <i class="fa fa-caret-down"></i>
  Cardio
</button>
    <div class="dropdown-content">
      <a @click.prevent="$emit('filter-workouts', 'cycling')">Cycling🚵</a>
      <a
  @click.prevent="$emit('filter-workouts', 'running')"
>
  Running🏃‍♂️
</a>
      <a href="#" @click.prevent="$emit('filter-workouts', 'swimming')">
  Swimming🏊
</a>
    </div>
    </div>
   
</div>
</nav>
</template>

<style>


.navbar {

  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  background-color: #2168aa;
  
}

.navbar a {
  font-size: 16px;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}


.dropdown {
  overflow: hidden;
}

.all-btn{
 font-size: 16px;  
  border: none;
  outline: none;
  color: white;
  padding: 14px 16px;
  background-color: inherit;
  font-family: inherit;
  margin-left:20px;
  margin-right:20px;
  align-items: center;
  justify-content: center;
  cursor:pointer;
}

.dropdown .dropbtn {
  font-size: 16px;  
  border: none;
  outline: none;
  color: white;
  padding: 14px 16px;
  background-color: inherit;
  font-family: inherit;
  margin-left:20px;
  margin-right:20px;
  align-items: center;
  justify-content: center;
}

.navbar a:hover, .dropdown:hover .dropbtn, .all-btn:hover {
  background-color: red;
}

.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
  cursor:pointer
}

.dropdown-content a {
  float: none;
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  text-align: left;
}

.dropdown-content a:hover {
  background-color: #ddd;
}

.dropdown:hover .dropdown-content {
  display: block;
}

</style>