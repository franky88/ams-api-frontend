<template>
  <div class="row">
    <div class="col-sm-12">
      <StudentData/>
    </div>
  </div>
</template>

<script>
import StudentData from './components/StudentsData.vue'
export default {
  name: 'App',
  components: {
    StudentData
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
