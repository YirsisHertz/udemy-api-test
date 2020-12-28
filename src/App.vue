<template>
  <HelloWorld />
  <hr />
  
  <h2> Mis Cursos </h2>

  <div v-for="course in courses" :key="course.id" > 
    <div class="container">
      <strong class="course-name"> {{course.title}} </strong>
      <br />
      <br />
      <span class="ox-alert alert-dark ox-alert-flat"> Instructor: {{course.visible_instructors[0].title}} </span>
      <br />
      <span class="ox-alert alert-danger ox-alert-flat"> Lenguaje: {{course.visible_instructors[0].locale}}</span>
      <br />

      <p> <a target="_blank" :class="[course.is_paid ? `ox-btn ox-btn-success ox-btn-rounded` : `ox-btn ox-btn-warn ox-btn-rounded`]" :href="`https://www.udemy.com${course.url}`"> {{course.is_paid ? "Comprar Curso" : "Curso Gratuito"}} </a> </p>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data(){
    return {
      courses: [],
    }
  },
  components: {
    HelloWorld
  },
  created(){
    this.getData()
  },
  methods:{
    
    async getData(){

      const url = "https://www.udemy.com/instructor-api/v1/taught-courses/courses/"

      const myHeaders = new Headers();

      myHeaders.append('Content-Type', 'application/json');
      myHeaders.append('Authorization', 'bearer {secret_key}';

      try{
	const fetchData = await fetch(url, {
	  method: 'GET',
	  headers: myHeaders,
	})
	const jsonData = await fetchData.json()

	const res = jsonData.results
  
        /* console.log(res) */
	this.courses = res
      }catch(err){
      	console.log(err)
      }
      
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}

h2{
	margin-top: 9px;
}

.container{
  background-color: #eee;
  margin: 3rem;
  padding: 1rem;
  border-radius: 3px;
  overflow: hidden;
}

.course-name{
	font-size: 1.3rem;
}

::-webkit-scrollbar {
  width: 5px;
  height: 5px;
}
::-webkit-scrollbar-button {
  width: 0px;
  height: 0px;
}
::-webkit-scrollbar-thumb {
  background: #b0b0b0;
  border: 0px none #ffffff;
  border-radius: 50px;
}
::-webkit-scrollbar-thumb:hover {
  background: #b5b5b5;
}
::-webkit-scrollbar-thumb:active {
  background: #545454;
}
::-webkit-scrollbar-track {
  background: #8f8f8f;
  border: 0px none #ffffff;
  border-radius: 50px;
}
::-webkit-scrollbar-track:hover {
  background: #5c5c5c;
}
::-webkit-scrollbar-track:active {
  background: #787878;
}
::-webkit-scrollbar-corner {
  background: transparent;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
